FROM nginx:1.19
LABEL author "Melvin Versluijs <https://github.com/melvinversluijs>"
RUN apt-get -y update

## Copy initial magento files.
COPY ./magento/ /var/www/html

## Copy SSL certificates.
COPY ./docker/nginx/certs/*  /etc/ssl/

## Copy nginx site configuration file.
COPY ./docker/nginx/magento.conf /etc/nginx/conf.d/site.conf