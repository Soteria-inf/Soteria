# OAuth2 Proxy - Installation et configuration

## Prerequis

- LXC ou VM sous Debian
- Docker installe
- Keycloak operationnel (fournisseur d'identite OIDC)

## Organisation des fichiers

```
/opt/oauth2-proxy/
├── docker-compose.yml
├── .env
└── ...
```

## Docker Compose

Pour une instance unique d'OAuth2 Proxy :

```yaml
services:
  oauth2-proxy:
    image: quay.io/oauth2-proxy/oauth2-proxy:latest
    container_name: oauth2-proxy
    restart: unless-stopped
    env_file:
      - .env
    ports:
      - "4180:4180"
```

## Variables d'environnement

Creer le fichier `.env` :

```
# Keycloak (OIDC)
OAUTH2_PROXY_PROVIDER=keycloak-oidc
OAUTH2_PROXY_CLIENT_ID=CHANGE_ME
OAUTH2_PROXY_CLIENT_SECRET=CHANGE_ME
OAUTH2_PROXY_REDIRECT_URL=https://webserv.<DOMAIN>/oauth2/callback
OAUTH2_PROXY_OIDC_ISSUER_URL=https://<KEYCLOAK_DOMAIN>/realms/<REALM_NAME>

# Cookie
OAUTH2_PROXY_COOKIE_SECRET=CHANGE_ME
OAUTH2_PROXY_COOKIE_SECURE=true
OAUTH2_PROXY_COOKIE_NAME=_oauth2_proxy

# Autoriser tous les emails (a restreindre en production)
OAUTH2_PROXY_EMAIL_DOMAINS=*

# TLS (certificats auto-signes)
OAUTH2_PROXY_SSL_INSECURE_SKIP_VERIFY=true
OAUTH2_PROXY_HTTP_ADDRESS=0.0.0.0:4180
OAUTH2_PROXY_REVERSE_PROXY=true
OAUTH2_PROXY_SET_XAUTHREQUEST=true

# Divers
OAUTH2_PROXY_SKIP_PROVIDER_BUTTON=true
```

> **Note** : Pour un OAuth2 Proxy par application, creer plusieurs services dans le `docker-compose.yml` avec des fichiers `.env` et ports differents.

## Rappels de securite

- Remplacer `OAUTH2_PROXY_COOKIE_SECRET` par une valeur longue et aleatoire
- Restreindre `OAUTH2_PROXY_EMAIL_DOMAINS` aux domaines autorises
- Limiter l'exposition du port 4180 au reseau d'administration
