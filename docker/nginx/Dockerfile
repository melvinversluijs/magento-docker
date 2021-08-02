FROM nginx:1.21-alpine
MAINTAINER "Melvin Versluijs <https://github.com/melvinversluijs>"
RUN apk update

## Copy SSL certificates.
COPY ./docker/nginx/certs/*  /etc/ssl/

## Copy nginx site configuration file.
COPY ./docker/nginx/magento.conf /etc/nginx/conf.d/site.conf