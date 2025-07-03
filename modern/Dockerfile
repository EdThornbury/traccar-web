FROM node:18-alpine AS build

WORKDIR /app

COPY package.json .

RUN npm install --legacy-peer-deps

RUN npm i -g serve

COPY . .

RUN npm run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
COPY --from=build /app/nginx-split.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
# Uncomment the following line if you want to serve the build directory directly
# This is useful if you want to use a different server like serve or http-server
#CMD [ "serve", "-s", "build" ]
