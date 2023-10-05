FROM php:8.2-fpm-bullseye AS base
SHELL ["/bin/bash", "-oeux", "pipefail", "-c"]

ENV COMPOSER_ALLOW_SUPERUSER=1 \
    COMPOSER_HOME=/composer

COPY --from=composer:2.6 /usr/bin/composer /usr/bin/composer

RUN apt-get update && \
    apt-get -y install --no-install-recommends locales git libicu-dev libonig-dev libzip-dev unzip libjpeg62-turbo-dev libpng-dev nodejs npm && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    docker-php-ext-configure gd --with-jpeg &&\
    docker-php-ext-install intl pdo_mysql zip bcmath gd && \
    composer config -g process-timeout 3600 && \
    composer config -g repos.packagist composer https://packagist.org && \
    localedef -f UTF-8 -i ja_JP ja_JP.UTF-8

RUN npm install n -g && \
    n 18.18.0

ENV LANG=ja_JP.UTF-8 \
    LANGUAGE=ja_JP:ja \
    LC_ALL=ja_JP.UTF-8 \
    TZ=Asia/Tokyo

COPY ./infra/php/php.ini /usr/local/etc/php/php.ini

EXPOSE 5173

WORKDIR /work/src