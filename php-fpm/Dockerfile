FROM php:8-fpm

RUN groupadd -g 1000 ubuntu; \
    useradd ubuntu -u 1000 -g 1000 -m -s /bin/bash

RUN mkdir /var/log/php/ && \
    touch /var/log/php/www.access.log && \
    touch /var/log/php/fpm-php.www.log && \
    chown ubuntu:ubuntu -R /var/log/php 

RUN set -eux; \
    apt update && \
    apt install -y \
    libmcrypt-dev \
    libwebp-dev \
    libjpeg-dev \
    libicu-dev \
    libzip-dev && \
    apt purge -y --auto-remove

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libpng-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd

RUN docker-php-ext-install \
    intl \
    zip \
    pdo_mysql


