FROM php:8.0-fpm

# Composer install
COPY --from=composer:2.0 /usr/bin/composer /usr/bin/composer

# install Node.js
COPY --from=node:10.22 /usr/local/bin /usr/local/bin
COPY --from=node:10.22 /usr/local/lib /usr/local/lib

RUN apt-get update && \
    apt-get -y install \
	libicu-dev \
    git \
    zip \
    unzip \
    vim \
	zlib1g-dev \ 
    libonig-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
	libpng-dev \
	libjpeg-dev \
	libzip-dev \
    && docker-php-ext-install \
        intl \
        pdo_mysql \ 
        bcmath \
        gd \
    && docker-php-ext-configure gd \
        --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \

    && docker-php-ext-install -j$(nproc) gd

COPY ./src /var/www/html/

WORKDIR /var/www/html

RUN composer global require "laravel/installer"

RUN chmod 777 -R storage