# Réponses du TP2

## Q1

Strapi utilise `DATABASE_CLIENT`, `DATABASE_HOST`, `DATABASE_PORT`, `DATABASE_NAME`, `DATABASE_USERNAME` et `DATABASE_PASSWORD`. Il accepte aussi `DATABASE_URL`. L'hôte est `postgres`, le nom du service Compose. `localhost` pointerait vers Strapi.

## Q2

`.env.example` indique les variables à configurer. `.env` contient les valeurs locales et les secrets. Git ignore ce fichier pour éviter de les publier.

## Q3

`docker compose down` supprime les conteneurs, mais garde les volumes. `docker compose down -v` supprime aussi les volumes et leurs données.

## Q4

Compose garde le signe `$` de `$$` pour le shell du conteneur. Le shell peut alors lire `POSTGRES_USER` et `POSTGRES_DB` pour le contrôle de santé.

## Q5

`postgres` est le nom du service Compose. `:ro` monte `servers.json` en lecture seule. `${PGADMIN_PORT:-5050}` prend 5050 si la variable est absente ou vide.

## Q6

`npm ci` reste en cache si `package.json` et `package-lock.json` ne changent pas. Après une modification dans `backend/config/`, Docker recopie le code et relance `npm run build`.

## Q7

`USER node` lance Strapi sans les droits de root. `--chown=node:node` donne à `node` la propriété des fichiers copiés.

## Q8

`service_healthy` attend que PostgreSQL soit prêt. Sans cette attente, Strapi peut démarrer trop tôt.

## Q9

Chaque article publié a deux lignes : un brouillon et une publication. Les trois articles ont donné six lignes.

## Q10

Dans le conteneur frontend, `localhost` désigne le frontend. Pour joindre Strapi, on utilise `http://strapi:1337`.

## Q11

Le Dockerfile a trois étapes. L'image finale contient le serveur standalone, ses dépendances nécessaires, les fichiers statiques et `public`. Sans `output: "standalone"`, le dossier attendu par le runner n'est pas créé et le `COPY` échoue. La taille n'a pas été notée. `docker images tp2/frontend` l'affiche.

## Q12

Strapi est sur les deux réseaux pour relier PostgreSQL au frontend. PostgreSQL n'est pas publié sur l'hôte.

## Q13

Générer les secrets et les garder dans un gestionnaire de secrets. Limiter les accès réseau et les droits de chaque service.

## Q14

`unless-stopped` redémarre le service après un crash. Docker le relance aussi au démarrage du moteur s'il n'a pas été arrêté manuellement. Après `docker compose stop` ou `kill`, il reste arrêté.
