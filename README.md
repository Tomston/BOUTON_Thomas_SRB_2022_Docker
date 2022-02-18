# Documentation du projet

## Qu'est-ce que Docker ?

Pour commencer, Docker est un logiciel permettant de lancer des applications dans des conteneurs logiciels. 
Un conteneur permet aux développeurs d'isoler les applications de leur environnement. En effet, un conteneur enveloppe une application et ses dépendances de façon à les isoler et pour les exécuter sur n'importe quel serveur.

Les points forts de Docker sont sa flexibilité et sa légèreté. En effet, les conteneurs Docker sont construits à partir des images Docker (quelques MB au minimum) et permettent aux développeurs de créer, déployer et exécuter efficacement des applications distribuées.

Cependant, il ne faut pas confondre la virtualisation et la conteneurisation. La conteneurisation est une forme plus légère qui s'appuie sur certaines parties de la machine hôte pour fonctionner.

![alt text](https://github.com/Tomston/Bouton_Thomas_SRB_2022_Docker/blob/main/Image.png)

Pour finir, les conteneurs permettent à une application d'être empaquetée et déplacée facilement, augmentant ainsi la simplicité d'une infrastructure.

> **Note** : https://fr.wikipedia.org/wiki/Docker_(logiciel)


## Fonctionnement de Docker

Le principe de fonctionnement de Docker est similaire à celui de LXC :
1. Des conteneurs en cours d'exécution partagent le même noyau Linux, ce qui les rend plus légers que des machines virtuelles.
2. Des conteneurs en cours d'exécution sont isolés les uns des autres et ont uniquement accès à une quantité limitée de ressources système.

> **Note** : https://www.ionos.fr/digitalguide/serveur/know-how/quest-ce-que-docker/

![alt text](https://github.com/Tomston/Bouton_Thomas_SRB_2022_Docker/blob/main/Image2.png)

> **Note** : LXC est un système de virtualisation utilisant l'isolation comme méthode de cloisonnement au niveau du système d'exploitation. Alors qu'un conteneur est un système logiciel.

Docker utilise le noyau Linux et des fonction de ce noyau pour séparer les processus afin qu'ils s'exécutent de façon independante.
Le but de cette séparation est d'optimiser l'utilisation de notre infrastructure, tout en bénéficiant du même niveau de sécurité que celui des systèmes distincts.

> **Note** : https://www.redhat.com/fr/topics/containers/what-is-docker#comment-fonctionne-la-technologie-docker


## Architecture du projet

Voici l'architecture du projet :
![alt text](https://github.com/Tomston/Bouton_Thomas_SRB_2022_Docker/blob/main/Image3.png)

Voici la liste des systèmes d'exploitation :
* Application : *Alpine Linux*
* API rest : *Alpine Linux*
* Base de données : *Compatible avec Linux, Windows et Mac*

De plus, voici ci-dessous la liste des ports utilisés :
* Port 3000: *utilisé par l'application*
* Port 8080: *utilisé par l'API rest*
* Port 27017: *utilisé par la base de données*

## Fonctionnement de l'architecture

L'application Node.js devra authentifier un utilisateur déjà inscrit et lui donner accès à un feed utilisateur.

Depuis l'application Web, l'utilisateur pourra s'inscrire en renseignons un email, un nom d'utilisateur et un mot de passe comme ci-dessous :

![alt text](https://github.com/Tomston/Bouton_Thomas_SRB_2022_Docker/blob/main/Image4.png)

À ce moment-là, l'application envoie une requête HTTP "POST" à l'API rest pour envoyer les données confidentielles du nouvel utilisateur à la base de données MongoDB. L'API se chargera de transmettre les données à la base de données et de renvoyer un fichier JSON au client (à l'application).

Ensuite, l'utilisateur renseigne l'email et le mot de passe qu'il avait créé lors de son inscription comme ci-dessous :

![alt text](https://github.com/Tomston/Bouton_Thomas_SRB_2022_Docker/blob/main/Image5.png)

À cette étape, l'application envoie une requête HTTP "GET" à l'API rest pour vérifier que la ressource est bien présente dans la base de données MongoDB. L'API se chargera de vérifier l'existence de cette ressource et de renvoyer un fichier JSON au client (à l'application).

Lorsque les deux requêtes précédentes ont été réalisées, la connexion à l'application est établie et l'utilisateur pourra publier un post s'il le souhaite.

![alt text](https://github.com/Tomston/Bouton_Thomas_SRB_2022_Docker/blob/main/Image6.png)

Voici un schéma résumant le fonctionnement d'une API rest :

![alt text](https://github.com/Tomston/Bouton_Thomas_SRB_2022_Docker/blob/main/Image7.png)

> **Note** : https://www.redhat.com/fr/topics/api/what-is-a-rest-api

## Dockerfile

Un Dockerfile est un fichier qui contient une série de commandes ou d'instructions. Ces instructions sont exécutées dans l'ordre dans lequel elles sont écrites. L'exécution de ces instructions a lieu sur une image de base définit avec l'instruction "FROM".

> **Note** : Lors de la création du Dockerfile, les actions successives forment une nouvelle image à partir de l'image parente de base (c'est ce que l'on appelle "layers" ou "couches" en français)

Lorsque les instructions de notre Dockerfile sont définies, nous pouvons "build" ou tout simplement construire notre image Docker (personnalisée) à partir d'une commande Docker.
Nous pourrons ensuite créer un conteneur et lui assigner l'image que nous venons de créer avec notre Dockerfile.

Voici un schéma résumant l'utilisation du Dockerfile et de son image :

![alt text](https://github.com/Tomston/Bouton_Thomas_SRB_2022_Docker/blob/main/Image8.png)

> **Dockerfile pour l'application Node.js (commenté)** : https://github.com/Tomston/Bouton_Thomas_SRB_2022_Docker/blob/main/frontend/Dockerfile

> **Dockerfile pour l'API rest (commenté)** : https://github.com/Tomston/Bouton_Thomas_SRB_2022_Docker/blob/main/backend/Dockerfile

> **Note** : https://geekflare.com/fr/dockerfile-tutorial/

> **Note** : https://phoenixnap.com/kb/create-docker-images-with-dockerfile

## docker-compose.yml

Docker Compose est un logiciel utilisé pour définir et exécuter des applications Docker multi-conteneurs (cela évite de démarrer et de gérer manuellement chaque conteneur). Il fonctionne en appliquant les règles définies dans un fichier docker-compose.yaml.

Le fichier YAML configure les services de l'application et inclut des règles spécifiant la manière dont nous souhaitons qu'ils s'exécutent. Lorsque le fichier est créé, nous pouvons démarrer, arrêter ou reconstruire tous les services à l'aide d'une seule commande Docker.

> **Note** : Généralement, chaque service à son propre conteneur. D'où l'utilisation de docker-compose pour une application

> **docker-compose pour les 3 services (commenté)** : https://github.com/Tomston/Bouton_Thomas_SRB_2022_Docker/blob/main/docker-compose.yml

> **Note** : https://phoenixnap.com/kb/docker-compose

## Annexes

> **Node.JS** : Node.js est un environnement d’exécution JavaScript open source, multi-plateforme et back-end qui s’exécute sur le moteur V8 et exécute du code JavaScript en dehors d’un navigateur Web. Node.js permet aux développeurs d’utiliser JavaScript pour écrire des outils de ligne de commande et pour les scripts côtés serveurs, c’est-à-dire exécuter des scripts côté serveur pour produire du contenu de page Web dynamique avant que la page ne soit envoyée au navigateur Web de l’utilisateur.
> https://en.wikipedia.org/wiki/Node.js

> **React.JS** : React (également connu sous le nom de React.js ou ReactJS) est une bibliothèque JavaScript frontale gratuite et open-source permettant de créer des interfaces utilisateur basées sur des composants d’interface utilisateur. Il est maintenu par Meta (anciennement Facebook) et une communauté de développeurs individuels et d’entreprises. React peut être utilisé comme base dans le développement d’applications mono pages ou mobiles. Cependant, React ne concerne que la gestion des états et le rendu de cet état au DOM, de sorte que la création d’applications React nécessite généralement l’utilisation de bibliothèques supplémentaires pour le routage, ainsi que certaines fonctionnalités côté client.
> https://en.wikipedia.org/wiki/React_(JavaScript_library)

> **MongoDB** : MongoDB est un programme de base de données multi-plateforme orienté document disponible à la source. Classé comme un programme de base de données NoSQL, MongoDB utilise des documents de type JSON avec des schémas facultatifs. MongoDB est développé par MongoDB Inc. et sous licence SSPL (Server Side Public License).
> https://en.wikipedia.org/wiki/MongoDB
