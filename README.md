# Template Docker pour projet Bedrock

## Présentation du projet

Le but de ce modèle est de démarrer un projet WordPress avec une installation Bedrock simplement, j'ai créé ce petit
modèle de projet docker très simple. Il démarre trois conteneurs :

- un pour la base de données
- un pour le serveur web
- un pour php-fpm

Ces derniers sont réfléchis de sorte à rendre ce modèle facilement réutilisable et personnalisable.

## Comment démarrer un projet basé sur ce modèle ?

Si vous souhaitez utiliser cette installation, il vous suffit de cliquer sur le bouton "Use this template" et ainsi de
créer un projet sur GitHub, en remplissant comme à votre habitude le formulaire.

Vous devez ensuite copier le fichier `.env.dist.example` et le nommer `.env` pour pouvoir démarrer le projet Docker.
Pour démarrer le projet, vous devez avoir Docker d’installé et en cours d’exécution. Si vous êtes sous Linux vous pouvez
normalement vérifier l’état de Docker en tapant la commande

```shell
sudo systemctl status docker
```

Si docker n’est pas démarré vous pouvez le démarrer avec la commande suivante

```shell
sudo systemctl start docker
```

Si vous souhaitez activer docker au démarrage de votre système d’exploitation utilisez la commande suivante :

```shell
sudo systemctl enable docker
```

Une fois que vous avez vérifié que docker tourne bien sur votre machine, vous pouvez normalement construire le projet
avec la commande

```shell
docker-compose build
```

Et ensuite le démarrer avec la commande

```shell
docker-compose up
```

Vous pouvez alors accéder au projet en vous rendant sur à l’adresse http://localhost:4444.

## Personnaliser les variables d’environnement

### Base de données

Vous pouvez normalement utiliser directement ce modèle pour démarrer un projet. Je vous recommande cependant de modifier
la variable `MYSQL_CONTAINER_NAME` afin de bénéficier d’un nom de conteneur unique et éviter les risques de collisions
entre vos projets.

### WordPress

Les variables d’environnements WordPress permettent de choisir différents paramètres pour configurer son fonctionnement.
Les variables actuellement prises en compte par ce modèle Docker sont

```dotenv
WP_ENV='development'
WP_HOME='http://localhost:${NGINX_PORT}'
WP_SITEURL="${WP_HOME}/wp"
WP_DEBUG_LOG=/path/to/debug.log
```

La liaison avec la base de données se fait automatiquement dans le fichier `docker-compose.yml` et se base sur le nom du
conteneur de la base de données.
