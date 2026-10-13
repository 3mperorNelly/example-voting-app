FROM node:20-alpine AS base
WORKDIR /usr/local/app
COPY package*.json ./
RUN npm install && npm install -g nodemon && npm cache clean --force

FROM base AS dev
COPY . .
RUN chown -R node:node /usr/local/app
USER node
EXPOSE 80
CMD ["node", "server.js"]

FROM base AS final
COPY . .
RUN chown -R node:node /usr/local/app
USER node
EXPOSE 80
CMD ["node", "server.js"]
