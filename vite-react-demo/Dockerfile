# Etape de build
FROM node:lts as build-stage

WORKDIR /app

# Copie des fichiers de dépendances
COPY package*.json ./

# Installation des dépendances
RUN npm install

# Copie du reste des fichiers du projet
COPY . .

# Construction de l'application
RUN npm run build

# Etape de production
FROM nginx:stable-alpine as production-stage

# Copie du build depuis l'étape de build vers le dossier de serveur nginx
COPY --from=build-stage /app/dist /usr/share/nginx/html

# Exposition du port 80 pour l'accès au serveur HTTP
EXPOSE 80

# Commande pour démarrer nginx et garder le conteneur en fonctionnement
CMD ["nginx", "-g", "daemon off;"]
