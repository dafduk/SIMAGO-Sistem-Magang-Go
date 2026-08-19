FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# 1. Install PHP 8.3 dan tools dasar dari Ubuntu / PPA Ondrej
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

# 2. Install Composer LANGSUNG via script (Bypass docker.io/library/composer)
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /var/www

COPY . .

# 3. Install dependensi Laravel
RUN composer install --no-dev --optimize-autoloader || true

# 4. Atur permission folder storage
RUN chown -R www-data:www-data /var/www/storage /var/www/bootstrap/cache

EXPOSE 9000

# 5. Jalankan PHP-FPM
CMD ["php-fpm8.3", "-F"]
