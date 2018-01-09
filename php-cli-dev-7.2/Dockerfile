FROM php:7.2-cli-alpine
MAINTAINER Patrick Mosch <info@xuad.net>

ARG PHP_GROUP_ID=999
ARG PHP_USER_ID=999
ARG REMOTE_HOST=10.0.75.1
ARG IDE_KEY=docker-xdebug
ARG REMOTE_PORT=9001
ARG REMOTE_ENABLE=1
ARG SERVER_NAME=localhost

ENV TERM=xterm \
    TZ=Europe/Berlin \
    PHP_XDEBUG_REMOTE_HOST=${REMOTE_HOST} \
    PHP_XDEBUG_IDE_KEY=${IDE_KEY} \
    PHP_XDEBUG_REMOTE_PORT=${REMOTE_PORT} \
    PHP_XDEBUG_REMOTE_ENABLE=${REMOTE_ENABLE} \
    PHP_IDE_CONFIG="serverName=${SERVER_NAME}"

RUN apk update && apk add  --no-cache \
        shadow \
        bash \
        git \
        mysql-client \
        curl \
        mc \
        libintl \
        icu \K
        icu-dev \
        libxml2-dev \
        freetype \
        freetype-dev \
        libpng \
        libpng-dev \
        libjpeg-turbo \
        libjpeg-turbo-dev \
        g++ \
        make \
        autoconf && \
    rm /var/cache/apk/*

RUN pecl install xdebug-2.6.0beta1 && \
    docker-php-ext-configure gd \
        --with-freetype-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install gd && \
    docker-php-ext-install pdo_mysql pcntl intl && \
    docker-php-ext-configure intl && \
    addgroup -g ${PHP_GROUP_ID} php-user  && \
    adduser -D -u ${PHP_USER_ID} -G php-user php-user

RUN wget https://phar.phpunit.de/phpunit.phar && \
    chmod +x phpunit.phar && \
    mv phpunit.phar /usr/local/bin/phpunit

COPY conf/*.ini /usr/local/etc/php/conf.d/

WORKDIR /app
CMD ["php", "-a"]