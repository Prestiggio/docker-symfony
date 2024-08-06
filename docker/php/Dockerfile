FROM php:8.3-fpm

# Installe les dépendances système
RUN apt-get update && apt-get install -y \
    libicu-dev \
    libpq-dev \
    libzip-dev \
    libonig-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Installe les extensions PHP requises
RUN docker-php-ext-install intl pdo pdo_mysql zip opcache

# Installe Xdebug
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

# Installe Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Définit le répertoire de travail
WORKDIR /var/www/html

# Copie le fichier de configuration Xdebug
COPY ./docker/php/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini