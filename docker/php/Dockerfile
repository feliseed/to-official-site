FROM php:8.3-fpm

COPY php.ini /usr/local/etc/php/

# Install required PHP extensions and dependencies
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libonig-dev \
    libxml2-dev \
    libzip-dev \ 
    zip \
    unzip

# Configure PHP extensions
RUN docker-php-ext-configure gd --with-jpeg

# Install PHP extensions
# Pre-installed extensions of php:8.1-cli are below.
# Core
# ctype
# curl
# date
# dom
# fileinfo
# filter
# ftp
# hash
# iconv
# json
# libxml
# mbstring
# mysqlnd
# openssl
# pcre
# PDO
# pdo_sqlite
# Phar
# posix
# readline
# Reflection
# session
# SimpleXML
# sodium
# SPL
# sqlite3
# standard
# tokenizer
# xml
# xmlreader
# xmlwriter
# zlib
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd zip

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR /var/www/html

# Set user permissions
RUN chown -R www-data:www-data /var/www/html
