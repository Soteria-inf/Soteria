# BookStack - Installation

## Prerequis

- LXC ou VM avec Docker installe
- Keycloak operationnel (SSO OIDC)
- FreeIPA operationnel (annuaire utilisateurs)
- Caddy operationnel (reverse proxy)
- AdGuard operationnel (resolution DNS)

## Organisation des fichiers

```
/opt/bookstack/
├── docker-compose.yml
├── .env
├── certs/
│   └── caddy-cert.pem       # Certificat auto-signe de Caddy (si applicable)
└── volumes/
    ├── mysql/
    └── bookstack/
        ├── ...
        └── keys/             # Certificats auto-signes de BookStack
            ├── cert.crt
            └── cert.key
```

## Configuration du fichier .env

Creer le fichier `.env` avec les variables suivantes :

```
# --- Authentification OIDC (SSO) ---
AUTH_METHOD=oidc
OIDC_NAME=SSO
OIDC_CLIENT_ID=bookstack
OIDC_CLIENT_SECRET=CHANGE_ME
OIDC_ISSUER=https://<KEYCLOAK_DOMAIN>/realms/<REALM_NAME>
OIDC_ISSUER_DISCOVER=true

# --- Base de donnees ---
MYSQL_DATABASE=bookstack_db
MYSQL_USER=CHANGE_ME
MYSQL_PASSWORD=CHANGE_ME
MYSQL_ROOT_PASSWORD=CHANGE_ME
DB_DATABASE=bookstack_db
DB_USERNAME=CHANGE_ME
DB_PASSWORD=CHANGE_ME

# --- BookStack ---
APP_URL=https://<BOOKSTACK_DOMAIN>
APP_KEY=base64:CHANGE_ME
DB_CONNECTION=mysql
DB_HOST=bookstack_db
DB_PORT=3306

# --- Systeme ---
PUID=1000
PGID=1000
TZ=Europe/Paris

# --- Ports ---
BOOKSTACK_HTTP_PORT=9000
BOOKSTACK_HTTPS_PORT=9002
```

## Generation de la cle d'application

```bash
openssl rand -base64 32
```

Reporter la valeur generee dans `APP_KEY=base64:<VALEUR>`.

## Docker Compose

Creer le fichier `docker-compose.yml` :

```yaml
volumes:
  bookstack_db_data: {}
  bookstack_config: {}

services:
  bookstack_db:
    image: mysql:8.4
    container_name: bookstack_db
    env_file:
      - .env
    volumes:
      - ./volumes/mysql:/var/lib/mysql
    restart: unless-stopped

  bookstack:
    image: lscr.io/linuxserver/bookstack:latest
    container_name: bookstack
    env_file:
      - .env
    ports:
      - "${BOOKSTACK_HTTP_PORT}:80"
      - "${BOOKSTACK_HTTPS_PORT}:443"
    volumes:
      - ./volumes/bookstack:/config
      # Si certificat auto-signe (decommenter) :
      # - ./certs/caddy-cert.pem:/usr/local/share/ca-certificates/caddy-cert.pem:ro
    restart: unless-stopped
    depends_on:
      - bookstack_db
```

## Demarrage

```bash
docker compose up -d
```

## Rappels de securite

- Utiliser des secrets forts et uniques pour la base de donnees et OIDC
- Ne jamais committer le fichier `.env`
- Limiter l'exposition des ports aux reseaux necessaires
