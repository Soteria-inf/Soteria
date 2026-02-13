# Caddy - Installation et configuration

## Prerequis

- LXC ou VM sous Debian
- DNS configure (AdGuard) pour la resolution des noms de domaine

## Installation

Installation sur une distribution basee sur Debian (cf. [documentation officielle](https://caddyserver.com/docs/install#debian-ubuntu-raspbian)) :

```bash
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https curl
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
chmod o+r /usr/share/keyrings/caddy-stable-archive-keyring.gpg
chmod o+r /etc/apt/sources.list.d/caddy-stable.list
sudo apt update
sudo apt install caddy
```

Verifier l'etat du service :

```bash
systemctl status caddy
```

## Configuration

La configuration se situe dans le fichier **Caddyfile**, generalement dans `/etc/caddy/`.

### Exemple de Caddyfile simple (reverse proxy)

```
{
        # Desactive la creation automatique de certificats Let's Encrypt
        local_certs

        # Desactive la verification OCSP
        skip_install_trust
}

webserv.<DOMAIN> {
        # Reverse proxy vers le serveur web
        reverse_proxy <IP_WEBSERVER>:80

        log {
                output file /var/log/caddy/serveurweb.access.log
        }
}
```

### Validation et redemarrage

Valider la syntaxe du Caddyfile :

```bash
caddy validate --config /etc/caddy/Caddyfile
```

Redemarrer le service :

```bash
systemctl restart caddy
```

## Rappels de securite

- Restreindre l'acces au serveur Caddy aux seuls reseaux necessaires
- Utiliser des certificats valides en production
- Surveiller les logs d'acces et d'erreur
