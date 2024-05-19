FROM node:18.19-alpine

WORKDIR /usr/src/app

ENV PATH=/usr/src/node_modules/.bin:$PATH

ARG VITE_HOST="0.0.0.0"
ARG VITE_PORT="80"
ARG VITE_CLIENT_PORT="5000"
ENV VITE_HOST=$VITE_HOST
ENV VITE_PORT=$VITE_PORT
ENV VITE_CLIENT_PORT=$VITE_CLIENT_PORT
 

COPY package.json .

RUN npm install

COPY . .

CMD [ "npm","run","dev" ]
