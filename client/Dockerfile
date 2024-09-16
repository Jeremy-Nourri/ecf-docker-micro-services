FROM node:14 AS build

WORKDIR /app

COPY package*.json ./

RUN npm install \
    && npm update \
    && npm uninstall node-sass \
    && npm install sass

COPY . .

RUN npm run build

FROM node:14

WORKDIR /app

COPY --from=build /app/build /app/build
COPY server.js /app/server.js

COPY package*.json ./
RUN npm install

EXPOSE 3000

CMD ["npm", "start"]