# image de base node.js
FROM node:8.11-alpine

# copie la liste des dépendances qui sont présents dans le fichier package.json dans le dossier /app
# création du dossier /app s'il n'existe pas
COPY package.json /app/package.json

# installation de npm : gestionnaire de fichier sous node.js
# installation par défaut de tous les paquets présent dans package.json dont mongo (car aucun paquet spécifique n'est renseigné après npm install)
# déplacement dans le dossier /app
RUN cd /app && npm install

# copie le code applicatif dans le dossier /app/
COPY . /app/

# indique que le dossier d'exécution par défaut du conteneur sera /app
WORKDIR /app

# indique que le port d'écoute de l'application sera 8080
EXPOSE 8080

# commande exécuter : npm start, elle permet d'exécuter la commande de démarrage définit dans le fichier package.json
CMD ["npm", "start"]
