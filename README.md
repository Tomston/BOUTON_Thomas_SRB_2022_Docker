# Documentation du projet

## Qu'est-ce que Docker ?

Pour commencer, Docker est un logiciel permettant de lancer des applications dans des conteneurs logiciels. 
Un conteneur permet aux développeurs d'isoler les applications de leur environnement. En effet, un conteneur enveloppe une application et ses dépendances de façon à les isoler pour les exécuter sur n'importe quel serveur.

Les points forts de Docker sont sa flexibilité et sa légèreté. En effet, les conteneurs Docker sont construits à partir des images Docker (quelques MB au minimum) et permettent aux développeurs de créer, déployer et exécuter efficacement des applications distribuées.

Cependant, il ne faut pas confondre la virtualisation et la conteneurisation. La conteneurisation est une forme plus légère qui s'appuie sur certaines parties de la machine hôte pour fonctionner.

![alt text](https://github.com/Tomston/Bouton_Thomas_SRB_2022_Docker/blob/main/Image.png)

Pour finir, les conteneurs permettent à une application d'être empaquetée et déplacée facilement, augmentant ainsi la simplicité d'une infrastructure.

> **Note** : https://fr.wikipedia.org/wiki/Docker_(logiciel)


## Fonctionnement de Docker

Le principe de fonctionnement de Docker est simimaire à celui de LXC :
1. Des coneneurs en cours d'exécution partagent le même noyau Linux, ce qui les rend plus léger que des machines virtuelles.
2. Des conteneurs en cours d'exécution sont isolés les uns des autres et on uniquement accèes à une quantité limitée de ressources système.

> **Note** : https://www.ionos.fr/digitalguide/serveur/know-how/quest-ce-que-docker/

![alt text](https://github.com/Tomston/Bouton_Thomas_SRB_2022_Docker/blob/main/Image2.png)

> **Note** : LXC est un système de virtualisation utlisant l'isolation comme méthode de cloisennement au niveau du système d'exploitation. Alors qu'un conteneur est un système logiciel.

Docker utilise le noyau Linux et des fonction de ce noyau pour séparer les processus afin qu'ils s'exécutent de façon independante.
Le but de cette séparation est d'optimiser l'utilisation de notre infrastructure, tout en bénéficiant du même niveau se sécurité que celui des systèmes distincts.

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

Depuis l'application Web, l'utilisateur poura s'inscrire en renseignons un email, un nom d'utilisateur et un mot de passe comme ci-dessous :

![alt text](https://github.com/Tomston/Bouton_Thomas_SRB_2022_Docker/blob/main/Image4.png)

À ce moment là, l'application envoie une requêtte HTTP "POST" à l'API rest pour envoyer les données confidentielles du nouveau utilisateur à la base de données MongoDB. L'API se chargera de transmettre les données à la base de données et de renvoyer un fichier .JSON au client (à l'application).  

Ensuite, l'utilisateur renseigne l'email et le mot de passe qu'il avait créé lors de son inscription comme ci-dessous:

![alt text](https://github.com/Tomston/Bouton_Thomas_SRB_2022_Docker/blob/main/Image5.png)

À cette étape, l'application envoie une requête HTTP "GET" à l'API rest pour vérifier que la ressource est bien présente dans la base de données MongoDB. L'API se chargera de vérifier l'existence de cette ressource et de renvoyer un fichier .JSON au client (à l'application).

Lorsque les deux requêtes précédente ont été réalisés, la connexion à l'application est établi et l'utilisateur poura publier un post s'il le souhaite.

![alt text](https://github.com/Tomston/Bouton_Thomas_SRB_2022_Docker/blob/main/Image6.png)

Voici un schéma résumant le fonctionnement d'une API rest :

![alt text](https://github.com/Tomston/Bouton_Thomas_SRB_2022_Docker/blob/main/Image7.png)

> **Note** : https://www.redhat.com/fr/topics/api/what-is-a-rest-api

## Fonctionnement des Dockerfile

Voici un schéma résument le fonctionnement d'un Dockerfile

![alt text](https://github.com/Tomston/Bouton_Thomas_SRB_2022_Docker/blob/main/Image8.png)

## Fonctionnement du docker-compose.yml
