# Docker selon Aurélie Vache - Résumé des concepts essentiels

## Concepts fondamentaux

### Qu'est-ce que Docker ?
- **Containerisation** : Empaquetage d'applications avec leurs dépendances
- **Isolation** : Chaque conteneur est isolé du système hôte
- **Portabilité** : "Build once, run anywhere"
- **Légèreté** : Plus léger que les machines virtuelles

### Architecture Docker
- **Docker Engine** : Moteur de containerisation
- **Images** : Templates read-only pour créer des conteneurs
- **Conteneurs** : Instances d'images en cours d'exécution
- **Registry** : Stockage et distribution d'images (Docker Hub, etc.)

## Commandes essentielles

### Gestion des images
```bash
docker pull <image>          # Télécharger une image
docker build -t <tag> .      # Construire une image
docker images               # Lister les images
docker rmi <image>          # Supprimer une image
```

### Gestion des conteneurs
```bash
docker run <image>          # Créer et démarrer un conteneur
docker ps                   # Lister les conteneurs actifs
docker ps -a               # Lister tous les conteneurs
docker stop <container>     # Arrêter un conteneur
docker rm <container>       # Supprimer un conteneur
```

### Commandes utiles
```bash
docker exec -it <container> /bin/bash  # Accéder au conteneur
docker logs <container>                # Voir les logs
docker inspect <container>             # Informations détaillées
```

## Dockerfile - Bonnes pratiques

### Structure type
```dockerfile
FROM alpine:latest
WORKDIR /app
COPY . .
RUN apk add --no-cache nodejs npm
EXPOSE 3000
CMD ["node", "app.js"]
```

### Optimisations recommandées
- **Multi-stage builds** : Réduire la taille des images
- **Cache layers** : Optimiser l'ordre des instructions
- **.dockerignore** : Exclure les fichiers inutiles
- **Utilisateur non-root** : Sécurité

## Docker Compose

### Orchestration multi-conteneurs
```yaml
version: '3.8'
services:
  web:
    build: .
    ports:
      - "3000:3000"
    depends_on:
      - db
  db:
    image: postgres:13
    environment:
      POSTGRES_DB: myapp
```

### Commandes Compose
```bash
docker-compose up           # Démarrer les services
docker-compose down         # Arrêter et supprimer
docker-compose logs         # Voir les logs
docker-compose exec web sh  # Accéder à un service
```

## Sécurité et bonnes pratiques

### Sécurité
- Utiliser des images officielles
- Scanner les vulnérabilités
- Limiter les privilèges
- Secrets management

### Performance
- Optimiser la taille des images
- Utiliser des health checks
- Gérer les ressources (CPU, mémoire)

### Production
- Monitoring et logging
- Backup des données
- Stratégies de déploiement
- Orchestration (Kubernetes)

## Cas d'usage typiques

### Développement
- Environnements reproductibles
- Isolation des dépendances
- Tests automatisés

### Déploiement
- CI/CD pipelines
- Microservices
- Scalabilité horizontale

## Points clés à retenir

1. **Conteneurs ≠ VM** : Plus légers et rapides
2. **Immutabilité** : Les conteneurs ne changent pas
3. **Stateless** : Séparer l'application des données
4. **Logs centralisés** : Importante pour le monitoring
5. **Sécurité by design** : Intégrer dès le début

## Ressources complémentaires

- Documentation officielle Docker
- Best practices de sécurité
- Patterns microservices
- Migration vers Kubernetes

---

*Résumé basé sur les enseignements et bonnes pratiques promues par Aurélie Vache dans la communauté DevOps francophone.*


Plan de la premiere vidéo

Une image Docker c'est quoi ?
Docker est un outil de containerisation qui permet d'empaqueter une application et toutes ses dépendances dans une image. Cette image peut ensuite être déployée sur n'importe quel système compatible avec Docker.

Quel lien peut-elle avoir avec les layers ?
L'image Docker est composée de plusieurs couches (layers) qui représentent les différentes étapes de construction de l'image. Chaque instruction dans le Dockerfile crée une nouvelle couche, ce qui permet de réutiliser les couches existantes et d'optimiser le processus de construction.

Docker a t'il un cache ? a quoi sert-il ?
Oui, Docker utilise un système de cache pour accélérer le processus de construction des images. Lorsqu'une instruction dans le Dockerfile est exécutée, Docker vérifie si une couche correspondante existe déjà dans le cache. Si c'est le cas, il réutilise cette couche au lieu de la reconstruire, ce qui permet de gagner du temps et des ressources.

Comment lister des images ? Les lister avec des filtres ?
Pour lister les images Docker, vous pouvez utiliser la commande `docker images`. Pour filtrer les images, vous pouvez utiliser des options comme `--filter` pour n'afficher que les images correspondant à certains critères (par exemple, par nom ou par tag).

Les dangling images.
Comment supprimer mes images ?
Pour supprimer les images Docker, vous pouvez utiliser la commande `docker rmi <image>` en remplaçant `<image>` par l'ID ou le nom de l'image à supprimer. Pour supprimer toutes les images non utilisées (dangling images), vous pouvez utiliser la commande `docker image prune`.



Les layers Docker c'est quoi ? 
les layers sont des couches qui composent une image Docker. Chaque instruction dans le Dockerfile crée une nouvelle couche, ce qui permet de réutiliser les couches existantes lors de la construction de nouvelles images.
La relation avec les images Docker ?
Les images Docker sont constituées de plusieurs layers empilés les uns sur les autres. Chaque layer représente une modification ou une étape dans le processus de construction de l'image.
Parlons des layers intermediaires.
Comment lister les layers ?
Pour lister les layers d'une image Docker, vous pouvez utiliser la commande `docker history <image>` en remplaçant `<image>` par l'ID ou le nom de l'image. Cela affichera la liste des layers ainsi que les instructions qui ont été utilisées pour les créer.


Comment build une image docker?
Pour construire une image Docker, vous devez créer un fichier `Dockerfile` qui contient les instructions nécessaires à la construction de l'image. Ensuite, vous pouvez utiliser la commande `docker build -t <nom_image> <chemin_contexte>` pour construire l'image en spécifiant le nom de l'image et le chemin du contexte (généralement le répertoire contenant le Dockerfile).
le contexte de construction est l'ensemble des fichiers et répertoires accessibles à Docker lors de la construction de l'image. Il est important de bien définir ce contexte pour inclure toutes les dépendances nécessaires à votre application.

pour build à partir d'un Dockerfile spécifique, vous pouvez utiliser la commande suivante :

```bash
docker build -t <nom_image> -f <chemin_Dockerfile> <chemin_contexte>
```

Que faire avec les dangling images ?
Pour supprimer les images Docker, vous pouvez utiliser la commande `docker rmi <image>` en remplaçant `<image>` par l'ID ou le nom de l'image à supprimer. Pour supprimer toutes les images non utilisées (dangling images), vous pouvez utiliser la commande `docker image prune`.

Pour lister les images Docker, vous pouvez utiliser la commande `docker images`. Pour filtrer les images, vous pouvez utiliser des options comme `--filter` pour n'afficher que les images correspondant à certains critères (par exemple, par nom ou par tag).

Qu'est ce qu'un registry?
Un registry Docker est un service de stockage et de distribution d'images Docker. Il permet de stocker des images Docker de manière centralisée et de les partager facilement entre différents utilisateurs et environnements. Le registry par défaut utilisé par Docker est Docker Hub, mais il est également possible de configurer des registries privés pour des besoins spécifiques.
Avant de récupérer une image depuis un registry, vous devez vous assurer que vous êtes authentifié auprès de ce registry, surtout s'il s'agit d'un registry privé.
docker login
pour stocker nos images Docker dans un registry, vous pouvez utiliser la commande `docker push <nom_image>` en remplaçant `<nom_image>` par le nom de l'image que vous souhaitez pousser vers le registry.
pour récupérer une image depuis un registry, vous pouvez utiliser la commande `docker pull <nom_image>` en remplaçant `<nom_image>` par le nom de l'image que vous souhaitez récupérer.
pour récupérer  par exemple une image d'ubuntu, vous pouvez utiliser la commande suivante :
```bash
docker pull ubuntu
```
Pour taguer une image, vous pouvez utiliser la commande `docker tag <image_source> <image_destination>` en remplaçant `<image_source>` par l'ID ou le nom de l'image source et `<image_destination>` par le nom que vous souhaitez donner à l'image taguée.

 Afin de supprimer une image taguée, vous pouvez utiliser la commande `docker rmi <image_destination>` en remplaçant `<image_destination>` par le nom de l'image taguée que vous souhaitez supprimer.
 Cette commande supprimera uniquement l'image localement, sans affecter les autres copies de l'image qui pourraient exister dans un registry distant.



Les containers Docker
Un conteneur Docker est une instance d'une image Docker en cours d'exécution. Il s'agit d'un environnement léger et isolé qui exécute une application et ses dépendances. Les conteneurs partagent le noyau du système d'exploitation hôte, mais sont isolés les uns des autres, ce qui permet de les exécuter de manière sécurisée et efficace.

Pour créer un conteneur à partir d'une image, vous pouvez utiliser la commande `docker create <nom_image>`, en remplaçant `<nom_image>` par le nom de l'image que vous souhaitez utiliser. Cette commande crée un conteneur, mais ne le démarre pas.

Pour lister les conteneurs en cours d'exécution, vous pouvez utiliser la commande `docker ps`. Pour lister tous les conteneurs, y compris ceux qui sont arrêtés, vous pouvez utiliser `docker ps -a`.

Pour démarrer un conteneur à partir d'une image, vous pouvez utiliser la commande `docker run <nom_image>`, en remplaçant `<nom_image>` par le nom de l'image que vous souhaitez exécuter. Vous pouvez également ajouter des options à cette commande, par exemple pour publier des ports ou monter des volumes.

Pour arrêter un conteneur en cours d'exécution, vous pouvez utiliser la commande `docker stop <nom_conteneur>` en remplaçant `<nom_conteneur>` par l'ID ou le nom du conteneur que vous souhaitez arrêter.

Les options de créations
docker create --name <nom_conteneur> <nom_image> --<options>
--rm permet de supprimer automatiquement le conteneur lorsque celui-ci s'arrête.
--name permet de donner un nom au conteneur.
--detach permet de démarrer le conteneur en arrière-plan et de libérer le terminal.
--publish permet de publier un port du conteneur sur l'hôte.
--volume permet de monter un volume dans le conteneur.
--env permet de définir des variables d'environnement dans le conteneur.
--restart permet de définir la politique de redémarrage du conteneur.
--init permet d'exécuter un processus init à l'intérieur du conteneur.
-d permet de détacher le terminal du conteneur.
-P permet de publier tous les ports du conteneur sur des ports aléatoires de l'hôte.
-it permet d'exécuter le conteneur en mode interactif avec un terminal.
--cidfile permet de spécifier un fichier dans lequel l'ID du conteneur sera écrit.

Afin de se connecter à un conteneur en cours d'exécution, vous pouvez utiliser la commande `docker exec -it <nom_conteneur> /bin/bash`, en remplaçant `<nom_conteneur>` par le nom ou l'ID du conteneur. Cette commande ouvre un terminal interactif à l'intérieur du conteneur, vous permettant d'exécuter des commandes dans cet environnement.
`docker exec -d <nom_conteneur> <commande>` permet d'exécuter une commande dans un conteneur en arrière-plan.


Les volumes Docker
Les volumes Docker sont des espaces de stockage persistants qui peuvent être utilisés par les conteneurs pour stocker des données. Contrairement aux systèmes de fichiers des conteneurs, qui sont éphémères et disparaissent lorsque le conteneur est supprimé, les volumes sont gérés par Docker et peuvent être conservés même après la suppression des conteneurs.

Pour créer un volume Docker, vous pouvez utiliser la commande `docker volume create <nom_volume>`, en remplaçant `<nom_volume>` par le nom que vous souhaitez donner au volume.

Pour monter un volume dans un conteneur, vous pouvez utiliser l'option `--mount` lors de la création du conteneur, par exemple :
```bash
docker run --mount source=<nom_volume>,target=/chemin/dans/conteneur <nom_image>
```
Cela montera le volume spécifié à l'emplacement `/chemin/dans/conteneur` à l'intérieur du conteneur.

Pour lister les volumes Docker existants, vous pouvez utiliser la commande `docker volume ls`. Pour inspecter un volume spécifique, vous pouvez utiliser `docker volume inspect <nom_volume>`.

Pour supprimer un volume Docker, vous pouvez utiliser la commande `docker volume rm <nom_volume>`, en remplaçant `<nom_volume>` par le nom du volume que vous souhaitez supprimer. Notez que vous ne pouvez pas supprimer un volume qui est actuellement utilisé par un conteneur.

Pour lister les volumes utilisés par un conteneur, vous pouvez utiliser la commande `docker inspect <nom_conteneur>` et rechercher la section "Mounts" dans la sortie.

Pour attacher un volume déjà attaché à un conteneur à un autre conteneur, vous pouvez utiliser l'option `--volumes-from` lors de la création du nouveau conteneur, en spécifiant le nom ou l'ID du conteneur existant. Par exemple :
```bash
docker run --volumes-from <nom_conteneur_existant> <nom_image>
```
Cela permettra au nouveau conteneur d'accéder aux volumes montés dans le conteneur existant.

Pour monter le volume en lecture seule, vous pouvez ajouter l'option `:ro` à la fin de la spécification du volume, par exemple :
```bash
docker run --mount source=<nom_volume>,target=/chemin/dans/conteneur,readonly <nom_image>
```

Pour supprimer tous les volumes Docker non utilisés, vous pouvez utiliser la commande `docker volume prune`. Cette commande supprimera tous les volumes qui ne sont pas actuellement utilisés par un conteneur.

Les events
Les événements Docker sont des notifications générées par le moteur Docker pour signaler des changements d'état ou des actions effectuées sur les objets Docker, tels que les conteneurs, les images et les volumes. Vous pouvez utiliser la commande `docker events` pour afficher une liste en temps réel des événements Docker.

Par défaut, la commande `docker events` affichera tous les événements, mais vous pouvez filtrer les événements en fonction de différents critères, tels que le type d'objet (conteneur, image, volume) ou l'action (création, suppression, démarrage, arrêt). Par exemple, pour afficher uniquement les événements liés aux conteneurs, vous pouvez utiliser la commande suivante :
```bash
docker events --filter event=create --filter event=destroy
```
Cela affichera uniquement les événements de création et de destruction de conteneurs.

Les événements Docker peuvent être utiles pour surveiller l'activité de vos conteneurs et pour diagnostiquer des problèmes. Vous pouvez également utiliser des outils de gestion des journaux pour collecter et analyser les événements Docker de manière centralisée.

Pour afficher les événements des 5 derniers minutes, vous pouvez utiliser la commande suivante :
```bash
docker events --since 5m
```

filtrer les evenement d'un conteneur
```bash
docker events --filter container=<nom_conteneur>
```

filtrer les evenements liés à une image particulière
```bash
docker events --filter image=<nom_image>
```


Search
Lorsqu'on veut rechercher une image Docker, on peut utiliser la commande `docker search <nom_image>`. Cette commande interroge le registre Docker Hub pour trouver des images correspondant au nom spécifié.

```bash
docker search <nom_image>
```

pour rechercher dans un registre Docker privé, vous pouvez utiliser la commande `docker search` avec l'URL du registre. Par exemple :
```bash
docker search <nom_image> --registry <url_registre>
```

pour afficher les images non tronquées, vous pouvez utiliser l'option `--no-trunc` avec la commande `docker images`. Par exemple :
```bash
docker images --no-trunc
```

Le fichier .dockerignore

Le fichier `.dockerignore` est utilisé pour exclure des fichiers et des répertoires spécifiques lors de la construction d'une image Docker. Cela peut être utile pour réduire la taille de l'image et éviter d'inclure des fichiers inutiles.

Le fichier `.dockerignore` fonctionne de manière similaire à un fichier `.gitignore`. Vous pouvez spécifier des motifs de fichiers et de répertoires à ignorer. Par exemple, pour ignorer tous les fichiers `.log` et le répertoire `tmp`, vous pouvez créer un fichier `.dockerignore` avec le contenu suivant :
```yaml
*.log
tmp/
```

Passer des variables d'environnements dans un container.

```bash
docker run -e VAR_NAME=value <nom_image>
```
On peut définir des variables d'environnements à partir d'un fichier les contenant

```bash
docker run --env-file <chemin_vers_fichier_env> <nom_image>
```

il faut éviter de faire les 2 en meme temps, le -e prévaudra sur le --env-file.


Passer des arguments lors du build de l'image.

```bash
docker build --build-arg VAR_NAME=value -t <nom_image> <chemin_dockerfile>
```

On peut les définir dans un fichier Dockerfile avec l'instruction `ARG`.

```dockerfile
ARG VAR_NAME=default_value
FROM alpine 
```
ARG doit_etre_defini_avant_FROM si on veut qu'elle ait un effet sur cette derniere

si on utilise build arg malgré l'utilisation de ARG dans le Dockerfile, la valeur de build arg prévaudra sur la valeur par défaut définie dans le Dockerfile.

si on utilise la variable précédée de $ dans le Dockerfile, elle sera remplacée par la valeur de l'argument de construction.
exemple :
```dockerfile
ARG VAR_NAME=default_value
FROM alpine
RUN echo "La valeur de VAR_NAME est $VAR_NAME"
```
on pourra inclure VAR_NAME dans l'instruction RUN.
```bash
docker build --build-arg VAR_NAME=value -t <nom_image> <chemin_dockerfile>
```

Privileged Mode

par défaut, les conteneurs Docker s'exécutent en mode non privilégié, ce qui signifie qu'ils n'ont pas accès aux fonctionnalités du noyau de l'hôte. Cela améliore la sécurité en limitant les actions que les conteneurs peuvent effectuer.

Cependant, dans certains cas, il peut être nécessaire d'exécuter un conteneur en mode privilégié pour accéder à des fonctionnalités spécifiques, comme l'accès aux périphériques ou la modification des paramètres du noyau. Pour ce faire, vous pouvez utiliser l'option `--privileged` lors de l'exécution d'un conteneur.

```bash
docker run --privileged -it <nom_image>
```

ne surtout pas exécuter des conteneurs en mode privilégié sans raison valable, car cela peut exposer l'hôte à des risques de sécurité.

exemple de cas ou le mode privilégié peut être nécessaire :

- Accès aux périphériques : Si votre application nécessite un accès direct à des périphériques matériels (par exemple, des périphériques USB), vous devrez exécuter le conteneur en mode privilégié.
- Modification des paramètres du noyau : Certaines applications peuvent nécessiter des modifications des paramètres du noyau, ce qui n'est possible qu'en mode privilégié.


Debugging avec docker: toutes les commandes utiles
    docker logs <nom_container> --> permet d'afficher les logs d'un conteneur
    docker logs -f <nom_container> --> permet de suivre les logs d'un conteneur en temps réel
    docker port <nom_container> --> permet d'afficher les ports exposés par un conteneur
    docker exec -it <nom_container> /bin/bash --> permet d'ouvrir un terminal interactif dans un conteneur
    docker inspect <nom_container> --> permet d'afficher les détails d'un conteneur
    docker top <nom_container> --> permet d'afficher les processus en cours d'exécution dans un conteneur
    docker stats <nom_container> --> permet d'afficher les statistiques d'utilisation des ressources d'un conteneur
    docker events --filter event=die --> permet de suivre les événements de conteneurs qui se terminent
    docker events --filter image=<nom_image> --> permet de suivre les événements liés à une image spécifique
    docker run --entrypoint <nouvel_entrypoint> <nom_image> --<arguments> --> permet de remplacer l'entrypoint d'une image lors de l'exécution d'un conteneur  cela peut être utile pour le débogage ou pour exécuter des commandes spécifiques dans le conteneur.

    Exemple :
    docker run --entrypoint /bin/sh <nom_image> -c "ls /app" --> permet d'exécuter une commande spécifique dans le conteneur.

    
Docker clean et purge

permet de nettoyer les ressources Docker inutilisées, telles que les conteneurs arrêtés, les images non utilisées et les volumes orphelins. Cela peut aider à libérer de l'espace disque et à maintenir un environnement de développement propre.

Voici quelques commandes utiles pour nettoyer et purger les ressources Docker :

- Supprimer tous les conteneurs arrêtés :
```bash
docker container prune
```

- Supprimer toutes les images non utilisées :
```bash
docker image prune
```

- Supprimer tous les volumes orphelins :
```bash
docker volume prune
```

- Supprimer toutes les ressources inutilisées (conteneurs, images, volumes) :
```bash
docker system prune
```

- Supprimer toutes les ressources inutilisées, y compris les images non étiquetées :
```bash
docker system prune -a --volumes
```

on peut aussi utiliser rmi et rm pour supprimer des images et des conteneurs spécifiques :

- Supprimer une image :
```bash
docker rmi <nom_image>
```

- Supprimer un conteneur :
```bash
docker rm <nom_container>
```


Statistiques
la commande stats permet d'afficher les statistiques d'utilisation des ressources d'un conteneur en cours d'exécution. Cela inclut des informations sur l'utilisation du processeur, de la mémoire, du réseau et des disques.

```bash
docker stats <nom_container>
```
On peut aussi le faire en mode json
```bash
docker stats --format "{{json .}}" <nom_container>
```

ou détaché du temps réel
```bash
docker stats --no-stream <nom_container>
```


Copie et pause/unpause

```bash
docker cp <nom_container>:<chemin_source> <chemin_destination>
```

```bash
docker pause <nom_container>
```

```bash
docker unpause <nom_container>
```