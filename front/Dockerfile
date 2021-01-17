FROM node:latest as build-step
WORKDIR app/
COPY package*.json ./
COPY angular.json ./
COPY tsconfig*.json ./
COPY proxy.conf.json ./
RUN npm install && npm install -g @angular/cli
COPY ./src $HOME/app/src

#For deploying without Nginx
#EXPOSE 4200
#CMD [ "ng" , "serve" ]


RUN npm run build --prod --outputPath=./dist/tlcfront
FROM bunkerity/bunkerized-nginx as prod
#CMD ["rm","etc/nginx/redirect-http-to-https.conf"]
RUN apk --no-cache upgrade && \
    apk add --no-cache --virtual=run-deps \
      certbot \
      bash \
    && \
    rm -rf /tmp/* \
           /var/cache/apk/*  \
           /var/tmp/*
#Pour recuperer les certificats
VOLUME ["/etc/letsencrypt"]
COPY --from=build-step /app/dist/tlcfront/ /www