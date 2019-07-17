FROM php:7.2-fpm-stretch
LABEL author "Melvin Versluijs <https://github.com/melvinversluijs>"
RUN apt-get -y update
RUN apt-get -y install \
        libcurl4-gnutls-dev \
        zlib1g-dev \
        libpng-dev \
        libjpeg-dev \
        libfreetype6-dev \
        libxslt-dev

## Install libsodium, required as of Magento2.3.2
RUN curl -O https://download.libsodium.org/libsodium/releases/libsodium-1.0.18.tar.gz \
        && tar xfvz libsodium-1.0.18.tar.gz \
        && cd libsodium-1.0.18 \
        && ./configure \
        && make && make install \
        && pecl install -f libsodium    

## Configure GD
RUN docker-php-ext-configure \
        gd \
        --with-jpeg-dir=/usr/lib \
        --with-freetype-dir=/usr/include/freetype2

## Install required php modules.
RUN docker-php-ext-install \
        curl \
        pdo_mysql \
        xsl \
        zip \
        gd \
        bcmath \
        opcache \
        intl \
        soap

## Install composer globally.
RUN curl --silent --show-error https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

## Copy intial folder.
COPY ./magento /var/www/html

## Copy custom php ini file.
COPY ./docker/php/php_custom.ini /usr/local/etc/php/conf.d/php_custom.ini