# Start with the official Composer image and name it
FROM composer:2 AS composer

# Continue with the official PHP image
FROM php:rc-fpm

# Copy the Composer PHAR from the Composer image into the PHP image
COPY --from=composer /usr/bin/composer /usr/bin/composer

# Install
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libzip-dev \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install -j$(nproc) zip \
    && docker-php-ext-install -j$(nproc) opcache

RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

# Install xdebug
ARG WITH_XDEBUG=false
ARG XDEBUG_INI=/usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN \
     if $WITH_XDEBUG; then \
        pecl install xdebug; \
        docker-php-ext-enable xdebug; \
        echo "error_reporting = E_ALL" >> ${XDEBUG_INI}; \
        echo "display_startup_errors = 1" >> ${XDEBUG_INI}; \
        echo "display_errors = 1" >> ${XDEBUG_INI}; \
        echo "xdebug.remote_enable = 1" >> ${XDEBUG_INI}; \
        echo "xdebug.remote_autostart = 0" >> ${XDEBUG_INI}; \
        echo "xdebug.remote_connect_back = 0" >> ${XDEBUG_INI}; \
        echo "xdebug.max_nesting_level = 1500" >> ${XDEBUG_INI}; \
     fi ;

WORKDIR /app