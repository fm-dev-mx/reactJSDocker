FROM node:12.22.1-alpine3.11 as build-stage

WORKDIR /app/build

COPY ./package.json ./package.json
COPY ../nginx/nginx.conf ./nginx.conf

COPY ./packages/frontend1 ./packages/frontend1
COPY ./packages/ui-kit ./packages/ui-kit

RUN npm install -G corepack
RUN yarn init -2
RUN yarn add workspace ui-kit transpile

WORKDIR /app/build/packages/frontend1
RUN yarn add build

FROM emazzotta/docker-nginx-lua
COPY --from=build-stage /app/build/packages/frontend1/build /usr/share/nginx/html
COPY --from=build-stage /app/build/nginx/nginx.conf /etc/nginx/conf.d
