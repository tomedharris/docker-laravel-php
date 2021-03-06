FROM composer:latest as composer_install_laravel

WORKDIR /app

RUN composer create-project laravel/laravel .

FROM php:7.3-cli

# Install some updates.
RUN apt-get update -yqq \
    && apt-get install -y --no-install-recommends \
        wget \
        apt-utils \
        sqlite3 \
        libsqlite3-dev \
        libzip-dev \
        libpng-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libxml2-dev \
        libxslt-dev \
        redis-tools \
        httpie \
        sendmail \
    && rm -rf /var/lib/apt/lists/*

# Install some updates php extensions.
RUN docker-php-ext-install \
    pdo_sqlite \
    mysqli \
    pdo_mysql

# Install GD as some functional tests use it for creating fake file uploads.
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd xsl soap bcmath exif

RUN pecl install zip \
    && docker-php-ext-enable zip \
    && pecl install redis \
    && docker-php-ext-enable redis \
    && pecl install xdebug-2.7.2 \
    && docker-php-ext-enable xdebug

WORKDIR /app

COPY --from=composer_install_laravel /app .
