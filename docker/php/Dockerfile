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

# Install Xdebug
COPY ./xdebug.ini /usr/local/etc/php/conf.d/
RUN pecl install xdebug && \
    docker-php-ext-enable xdebug

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd zip

# Install imagick extension
# Use apt-get for Debian/Ubuntu-based images
RUN apt-get update && \
    apt-get install -y git build-essential libmagickwand-dev && \
    git clone https://github.com/Imagick/imagick.git --depth 1 /tmp/imagick && \
    cd /tmp/imagick && \
    git fetch origin master && \
    git switch master && \
    phpize && \
    ./configure && \
    make && \
    make install && \
    docker-php-ext-enable imagick && \
    apt-get remove --purge -y git && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/imagick


# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR /var/www/html

# Set user permissions
RUN chown -R www-data:www-data /var/www/html
