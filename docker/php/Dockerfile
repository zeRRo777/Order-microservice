FROM php:8.4-fpm

RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libpq-dev \
    libzip-dev \
    libmysqld-dev \
    libsqlite3-dev 
RUN docker-php-ext-install \ 
    pdo_pgsql \
    pdo_mysql \
    pdo_sqlite \
    zip opcache \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN pecl install redis \
    && docker-php-ext-enable redis \
    && pecl clear-cache

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN chmod +x /usr/bin/composer

WORKDIR /var/www

RUN chown -R www-data:www-data /var/www