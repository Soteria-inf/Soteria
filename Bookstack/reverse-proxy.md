# BookStack - Reverse proxy et certificats

## Liaison avec le reverse proxy

BookStack est accessible via le reverse proxy Caddy sans avoir a specifier le port dans l'URL. Se referer a la documentation [Caddy & OAuth2](../Caddy%20%26%20Oauth2/caddy-oauth2.md) pour la configuration.

## Certificat auto-signe

Si le reverse proxy utilise un certificat auto-signe, BookStack peut refuser la redirection vers Keycloak. Pour resoudre ce probleme :

1. Ajouter le volume dans `docker-compose.yml` :

```yaml
- ./certs/caddy-cert.pem:/usr/local/share/ca-certificates/caddy-cert.pem:ro
```

> **Important** : Creer le fichier et le dossier `certs/` **avant** de lancer le conteneur. Docker peut creer un dossier `caddy-cert.pem` a la place d'un fichier, ce qui provoque un conflit.

2. Recuperer le certificat racine depuis le serveur Caddy :

```bash
cat /var/lib/caddy/.local/share/caddy/pki/authorities/local/root.crt
```

3. Copier le contenu dans `./certs/caddy-cert.pem`

4. Se connecter au conteneur et mettre a jour les certificats :

```bash
docker exec -it bookstack /bin/sh
cp /usr/local/share/ca-certificates/caddy-cert.pem /usr/local/share/ca-certificates/caddy-cert.crt
update-ca-certificates
exit
docker compose restart
```

> **Note** : Cette operation doit etre repetee apres chaque `docker compose down && docker compose up -d`.
