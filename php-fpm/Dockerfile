FROM php:8-fpm AS base

RUN set -eux; \
    apt update && \
    apt install -y \
    libmcrypt-dev \
    libwebp-dev \
    libjpeg-dev \
    libicu-dev \
    libzip-dev && \
    rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libpng-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd

RUN docker-php-ext-configure gd --with-jpeg --with-webp --with-freetype

RUN docker-php-ext-install \
    gd \
    intl \
    zip \
    pdo_mysql

RUN set -eux; \
    docker-php-ext-enable opcache

FROM base AS php-fpm-dev

RUN groupadd -g 1000 hostgroup; \
    usermod -a -G hostgroup www-data

RUN pecl install xdebug
RUN docker-php-ext-enable xdebug
COPY xDebug.ini /usr/local/etc/php/conf.d/xdebug.ini

RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini
RUN sed -i '/cgi.fix_pathinfo=1/s/^;//g' /usr/local/etc/php/php.ini