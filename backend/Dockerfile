FROM php:8.2-fpm

# 1. Install system dependencies
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    git \
    curl

# 2. Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# 3. Install PHP extensions
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd

# 4. Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# 5. Set working directory
WORKDIR /var/www

# 6. Copy application files
COPY . /var/www

# 7. Install dependencies (FIXED: Added --no-scripts to prevent crashes)
RUN composer install --no-dev --optimize-autoloader --no-scripts

# 8. Fix permissions
RUN chown -R www-data:www-data /var/www \
    && chmod -R 775 /var/www/storage

CMD ["php-fpm"]