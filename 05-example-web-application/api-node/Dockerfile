# Progressively developed docker file, to allow notes to be developed.

# FROM docker.io/ubuntu:latest

# RUN apt update

# RUN apt install -y nodejs

#-------------------
# removing unecessary layers

# FROM docker.io/ubuntu
    
# RUN apt update && apt install -y nodejs

#-------------------
# how are we going to get our app into the container

# FROM docker.io/ubuntu

# RUN apt update && apt install -y nodejs npm

# COPY . .

# RUN npm install

# CMD ["npm", "run", "dev"]

#-------------------
# using a built node image will save having to install node and npm

# FROM docker.io/node:19.6-alpine

# COPY . .

# RUN npm install

# CMD ["npm", "run", "dev"]

#-------------------
# rather than copying the entire source directory, we can refine that.

# FROM docker.io/node:19.6-alpine

# COPY package*.json ./

# RUN npm install

# COPY . .

# CMD ["npm", "run", "dev"]

#-------------------
# we are going to organise things by putting things in subdirectories rather than the root
# NB: the use of the .dockerignore file is recommended to avoid copying unnecessary files
# we also productionise the cmd

# FROM docker.io/node:19.6-alpine

# WORKDIR /usr/src/app

# COPY package*.json ./

# RUN npm install

# COPY ./src .

# CMD ["node", "index.js"]

#-------------------
# improve security by excecuting as a not root user

# FROM docker.io/node:19.6-alpine

# WORKDIR /usr/src/app

# COPY package*.json ./

# RUN npm install

# USER node

# COPY --chown=node:node ./src .

# CMD ["node", "index.js"]

#-------------------
# use the production mode for the container
# use a clean install, a more repeatable build
# do not use the dev dependencies

# FROM docker.io/node:19.6-alpine

# WORKDIR /usr/src/app

# ENV NODE_ENV=production

# COPY package*.json ./

# RUN npm ci --only=production

# USER node

# COPY --chown=node:node ./src .

# CMD ["node", "index.js"]

#-------------------
# EXPOSE port 3000, effectively documentation
# and use a cache for the npm install

# FROM docker.io/node:19.6-alpine

# WORKDIR /usr/src/app

# EXPOSE 3000

# ENV NODE_ENV=production

# COPY package*.json ./

# RUN --mount=type=cache,target=/usr/src/app/.npm \
#   npm set cache /usr/src/app/.npm && \
#   npm ci --only=production

# USER node

# COPY --chown=node:node ./src .

# CMD ["node", "index.js"]

#-------------------
# EXPOSE port 3000, effectively documentation
# and use a cache for the npm install

FROM docker.io/node:lts-alpine

WORKDIR /usr/src/app

EXPOSE 3000

ENV NODE_ENV=production

COPY package*.json ./

RUN --mount=type=cache,target=/usr/src/app/.npm \
  npm set cache /usr/src/app/.npm && \
  npm ci --only=production

USER node

COPY --chown=node:node ./src .

CMD ["node", "index.js"]