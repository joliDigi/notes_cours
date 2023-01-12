# day 15

## Docker compose

Premier level d'orchestration

permet de créer plusieurs conteneurs

docker-compose.yml :

```yml
version: '3.3'
services:
  php:
    build: 
      context: .
    ports:
      - "8181:80"
    volumes:
      - ./code:/var/www/html
  db:
    image: mariadb:latest
    environment:
      - MARIA_ROOT_PASSWORD=admin
      - MARIADB_DATABASE=bdd
```

`docker compose version`

`docker compose up`

utilise le nom du conteneur db créé automatiquement comme Database Host