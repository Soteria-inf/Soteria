# BookStack - Depannage

## Changement d'APP_URL

Si le changement d'URL rend le site inaccessible, nettoyer le cache :

```bash
docker exec -it bookstack php /app/www/artisan config:clear
docker exec -it bookstack php /app/www/artisan cache:clear
docker exec -it bookstack php /app/www/artisan view:clear
```

Puis relancer :

```bash
docker compose down
docker compose up -d
```

## Acces aux logs

```bash
docker logs bookstack
docker logs bookstack_db
```
