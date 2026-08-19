FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# Install PHP 8.3 dan dependensi dari repository Ubuntu/Ondrej
RUN apt-get update && apt-get install -y \
    software-properties-common \
    curl unzip git zip \
    && add-apt-repository ppa:ondrej/php -y \
    && apt-get update && apt-get install -y \
    php8.3-fpm \
    php8.3-cli \
    php8.3-mysql \
    php8.3-mbstring \
    php8.3-xml \
    php8.3-bcmath \
    php8.3-curl \
    php8.3-gd \
    php8.3-zip \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

WORKDIR /var/www

COPY . .

RUN composer install --no-dev --optimize-autoloader || true

RUN chown -R www-data:www-data /var/www/storage /var/www/bootstrap/cache

EXPOSE 9000

# Jalankan PHP-FPM 8.3
CMD ["php-fpm8.3", "-F"]
