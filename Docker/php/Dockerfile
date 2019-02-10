FROM php:7.2-fpm
LABEL author "Melvin Versluijs <melvin.verslijs@outlook.com>"
RUN apt-get -y update
RUN apt-get -y install \
        libcurl4-gnutls-dev \
        zlib1g-dev \
#         libmcrypt-dev \
#         libpng12-dev \
        libjpeg-dev \
        libfreetype6-dev \
#         libxml2-dev \
        libxslt-dev
#         libicu-dev \
#         php-soap \
#         g++
# RUN docker-php-ext-configure \
#         intl
RUN docker-php-ext-configure \
        gd \
        # --enable-gd-native-ttf \
        --with-jpeg-dir=/usr/lib \
        --with-freetype-dir=/usr/include/freetype2
RUN docker-php-ext-install \
        curl \
        # mcrypt \
        # mysqli \
        pdo_mysql \
        xsl \
        zip \
        gd \
        bcmath \
        opcache \
        intl \
        soap
RUN curl --silent --show-error https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer