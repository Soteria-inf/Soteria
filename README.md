## Soteria

[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

> Conception, virtualisation et securisation d'une infrastructure d'entreprise, services critiques et simulations d'attaques.

## Presentation

**Soteria** est un projet de fin d'étude (PFE) visant a concevoir, deployer et securiser une infrastructure d'entreprise virtualisee. Il integre des services critiques (annuaire, DNS, serveur web) et valide leur resilience face a des attaques reseau et physiques.

## Problematique

Comment concevoir, deployer et securiser une infrastructure d'entreprise virtualisee, integrant des services critiques, tout en validant sa resilience face a des attaques reseau et physiques ?

## Objectifs

- Deployer une infrastructure virtualisee complete sur Proxmox
- Mettre en place des services critiques : FreeIPA (annuaire/AD), DNS (AdGuard), reverse proxy (Caddy), SSO (Keycloak), wiki (BookStack), VPN (WireGuard), pare-feu (OPNsense), serveur web (Nginx)
- Appliquer les bonnes pratiques de securite : segmentation reseau (VLAN), Zero Trust, moindre privilege, durcissement des configurations
- Simuler des attaques internes et externes pour tester la resilience
- Documenter l'ensemble de l'architecture, des configurations et des procedures

## Architecture

L'infrastructure repose sur les composants suivants :

| Composant | Role | Documentation |
|-----------|------|---------------|
| Proxmox | Hyperviseur / Virtualisation | [Proxmox](Proxmox/proxmox.md) |
| OPNsense | Pare-feu / Routeur / DHCP / VLAN | [OPNsense](OPNSENSE/opnsense.md) |
| FreeIPA | Annuaire LDAP / Kerberos / DNS interne | [FreeIPA](FreeIPA/freeipa.md) |
| Keycloak | SSO / Gestion des identites (OIDC) | [Keycloak](Keycloak/keycloak.md) |
| Caddy + OAuth2 Proxy | Reverse proxy / Authentification | [Caddy & OAuth2](Caddy%20%26%20Oauth2/caddy-oauth2.md) |
| BookStack | Wiki / Documentation interne | [BookStack](Bookstack/bookstack.md) |
| AdGuard Home | DNS / Filtrage DNS | [DNS AdGuard](DNS%20Adguard/dns-adguard.md) |
| WireGuard | VPN | [WireGuard VPN](Wireguard%20VPN/wireguard-vpn.md) |
| Nginx | Serveur web | [Nginx](Nginx/nginx-plV.md) |
| Zorin OS | Poste client | [PC Zorin OS](PC%20(Zorin%20OS)/pc-zorin-os.md) |

## Index des guides

### Socle et infrastructure

- [Proxmox](Proxmox/proxmox.md)
- [OPNsense](OPNSENSE/opnsense.md)
  - [Aliases et nomenclature](OPNSENSE/aliases.md)
  - [VLAN](OPNSENSE/vlan.md)
  - [DHCP et DNS](OPNSENSE/dhcp-dns.md)
  - [Depannage](OPNSENSE/troubleshooting.md)

### Identite et SSO

- [FreeIPA](FreeIPA/freeipa.md)
  - [Installation serveur](FreeIPA/installation.md)
  - [Joindre un poste client](FreeIPA/client-join.md)
  - [Administration](FreeIPA/administration.md)
- [Keycloak](Keycloak/keycloak.md)

### Reverse proxy et authentification

- [Caddy & OAuth2 Proxy](Caddy%20%26%20Oauth2/caddy-oauth2.md)
  - [Caddy - Installation et configuration](Caddy%20%26%20Oauth2/caddy.md)
  - [OAuth2 Proxy - Installation et configuration](Caddy%20%26%20Oauth2/oauth2-proxy.md)
  - [Integration Caddy + OAuth2 Proxy](Caddy%20%26%20Oauth2/integration.md)

### Services applicatifs

- [BookStack](Bookstack/bookstack.md)
  - [Installation et configuration](Bookstack/installation.md)
  - [SSO OIDC avec Keycloak](Bookstack/oidc.md)
  - [Reverse proxy et certificats](Bookstack/reverse-proxy.md)
  - [Migration](Bookstack/migration.md)
  - [Depannage](Bookstack/troubleshooting.md)
- [Nginx](Nginx/nginx-plV.md)
- [DNS AdGuard](DNS%20Adguard/dns-adguard.md)
- [WireGuard VPN](Wireguard%20VPN/wireguard-vpn.md)

### Poste client

- [PC Zorin OS](PC%20(Zorin%20OS)/pc-zorin-os.md)

## Methodologie

Le projet suit une approche experimentale et iterative :

1. **Analyse et conception** : definition de l'architecture cible, choix des technologies, identification des menaces
2. **Mise en place** : installation de Proxmox, deploiement des VM/LXC, configuration reseau
3. **Implementation des services** : FreeIPA, DNS, DHCP, serveur web, SSO, pare-feu
4. **Securisation** : Zero Trust, segmentation, gestion des privileges, durcissement
5. **Phase offensive** : tests d'intrusion internes et physiques
6. **Phase defensive** : detection, contre-mesures, amelioration
7. **Documentation** : redaction complete, presentation et demonstration

## Structure du depot

```
Soteria/
├── README.md                  # Ce fichier
├── LICENSE                    # CC BY-NC-SA 4.0
├── Proxmox/                   # Documentation Proxmox
├── OPNSENSE/                  # Documentation OPNsense
├── FreeIPA/                   # Documentation FreeIPA
├── Keycloak/                  # Documentation Keycloak
├── Caddy & Oauth2/            # Documentation Caddy + OAuth2 Proxy
├── Bookstack/                 # Documentation BookStack
├── DNS Adguard/               # Documentation AdGuard Home
├── Wireguard VPN/             # Documentation WireGuard
├── Nginx/                     # Documentation Nginx
└── PC (Zorin OS)/             # Documentation poste client
```

## Licence

Ce projet est sous licence [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).
Vous etes libre de partager et adapter ce contenu a condition de citer l'auteur, de ne pas en faire un usage commercial et de redistribuer sous la meme licence.
