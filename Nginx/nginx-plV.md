# Nginx

Serveur web utilise pour heberger les sites et applications web de l'infrastructure.

## Prerequis

- LXC ou VM sous Debian
- Acces root ou sudo

## Installation

Sur une machine Debian :

```bash
sudo apt install nginx -y
```

## Verification

Verifier que le service fonctionne :

```bash
systemctl status nginx
```

Le service doit etre en etat **running**.

## Configuration

Le fichier de configuration principal se trouve dans `/etc/nginx/nginx.conf`. Les configurations de sites sont dans `/etc/nginx/sites-available/` avec des liens symboliques dans `/etc/nginx/sites-enabled/`.

### Tester la configuration

```bash
sudo nginx -t
```

### Recharger la configuration

```bash
sudo systemctl reload nginx
```

> **Note** : Dans cette infrastructure, Nginx est place derriere le reverse proxy Caddy. Se referer a la documentation [Caddy & OAuth2](../Caddy%20%26%20Oauth2/caddy-oauth2.md) pour la configuration du reverse proxy.

## Rappels de securite

- Mettre a jour Nginx regulierement
- Desactiver les modules non utilises
- Limiter l'acces aux ports via le pare-feu
