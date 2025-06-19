FROM php:8.3-fpm

# Set working directory
WORKDIR /var/www/html

# Install dependencies
RUN apt-get update && apt-get install -y \
    git unzip curl libzip-dev libpng-dev libjpeg-dev libfreetype6-dev \
    libxml2-dev libonig-dev libicu-dev libxslt-dev libmagickwand-dev \
    libcurl4-openssl-dev zlib1g-dev libreadline-dev libmcrypt-dev gnupg \
    && docker-php-ext-install pdo pdo_mysql mysqli intl zip soap xsl \
    bcmath opcache gd sockets \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && pecl install redis \
    && docker-php-ext-enable redis

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Copy custom PHP config
COPY custom-php.ini /usr/local/etc/php/conf.d/

EXPOSE 9000
