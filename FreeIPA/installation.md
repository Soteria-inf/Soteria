# FreeIPA - Installation serveur

## Prerequis

- VM avec un OS compatible : Rocky Linux, AlmaLinux, CentOS Stream, Fedora ou RHEL
- Sur Proxmox, configurer le type de CPU sur **host** si problème recontré durant l'installation.
- Adresse IP statique

## Mise a jour du systeme

```bash
sudo dnf update -y
sudo reboot
```

## Configuration reseau

Configurer une IP statique sur l'interface :

```bash
sudo nmcli con mod ens18 ipv4.addresses <IP_FREEIPA>/<MASK>
sudo nmcli con mod ens18 ipv4.gateway <IP_GATEWAY>
sudo nmcli con mod ens18 ipv4.dns "<IP_DNS_1> <IP_DNS_2>"
sudo nmcli con mod ens18 ipv4.method manual
```

Redemarrer l'interface :

```bash
sudo nmcli con down ens18
sudo nmcli con up ens18
```

## Configuration du nom d'hote

```bash
sudo hostnamectl set-hostname ipa.<DOMAIN>
```

Editer le fichier `/etc/hosts` et ajouter :

```
<IP_FREEIPA>   ipa.<DOMAIN>    ipa
```

## Installation de FreeIPA

```bash
sudo dnf install ipa-server ipa-server-dns -y
```

```bash
sudo ipa-server-install --setup-dns --forwarder=<IP_DNS_1> --forwarder=<IP_DNS_2>
```

## Configuration du pare-feu

```bash
sudo firewall-cmd --add-service={freeipa-ldap,freeipa-ldaps,dns,ntp,http,https,kerberos} --permanent
sudo firewall-cmd --reload
```

Verification :

```bash
sudo firewall-cmd --list-all
```

## Rappels de securite

- Restreindre l'acces a l'interface FreeIPA au reseau d'administration
- Utiliser des mots de passe forts pour les comptes privilegies
- Planifier des sauvegardes regulieres (clés, certificats, base LDAP)
