# # Base Image
# FROM php:8.2-apache


# # Install system dependencies
# RUN apt-get update && apt-get install -y \
#     git \
#     curl \
#     libpq-dev \
#     unzip \
#     libzip-dev \
#     zip \
#     && docker-php-ext-install pdo pdo_pgsql zip

# # Install Composer
# RUN echo "\e[1;33mInstall COMPOSER\e[0m"
# RUN cd /tmp \
#     && curl -sS https://getcomposer.org/installer | php \
#     && mv composer.phar /usr/local/bin/composer

# RUN docker-php-ext-install pdo pdo_mysql



# RUN apt-get update

# # Install useful tools
# RUN apt-get -y install apt-utils nano wget dialog vim

# # Install important libraries
# RUN echo "\e[1;33mInstall important libraries\e[0m"
# RUN apt-get -y install --fix-missing \
#     apt-utils \
#     build-essential \
#     git \
#     curl \
#     libcurl4 \
#     libcurl4-openssl-dev \
#     zlib1g-dev \
#     libzip-dev \
#     zip \
#     libbz2-dev \
#     locales \
#     libmcrypt-dev \
#     libicu-dev \
#     libonig-dev \
#     libxml2-dev
    



# # Install Postgre PDO
# RUN apt-get install -y libpq-dev \
#     && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
#     && docker-php-ext-install pdo pdo_pgsql pgsql


# # Set working directory
# WORKDIR /var/www

# # Copy Laravel application files into the container

# COPY ../laravel /var/www

# # Install PHP dependencies
# RUN composer install --optimize-autoloader --no-dev

# # Set permissions for storage and bootstrap/cache
# RUN chown -R www-data:www-data /var/www/storage /var/www/bootstrap/cache

# # Expose Laravel's default port for `php artisan serve`
# EXPOSE 8000:80

# # Start Laravel using `php artisan serve`
# CMD ["php", "artisan", "serve","--host=localhost", "--port=8000"]




# Base Image
FROM php:8.2-apache

# Enable Apache mod_rewrite for Laravel
RUN a2enmod rewrite

# Install system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    curl \
    unzip \
    zip \
    libpq-dev \
    libzip-dev \
    libicu-dev \
    libonig-dev \
    libxml2-dev \
    && docker-php-ext-install pdo pdo_pgsql pdo_mysql zip intl \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer

# Set working directory
WORKDIR /var/www/html

# Copy Laravel application files into the container
COPY ../laravel /var/www/html

# Install PHP dependencies
RUN composer install --optimize-autoloader --no-dev

# Set permissions for storage and bootstrap/cache
RUN chown -R www-data:www-data /var/www/html/storage /var/www/html/bootstrap/cache

# Expose port 80 for Apache
EXPOSE 80


# RUN php artisan migrate:fresh 
# RUN echo " DocumentRoot /var/www//public"> /etc/apache2/sites-available/000-default.conf
#                 DocumentRoot /var/www/public
#                 <Directory /var/www/public>
#                     Options Indexes FollowSymLinks
#                     AllowOverride All
#                     Require all granted
#                 </Directory>
#             </VirtualHost>" > /etc/apache2/sites-available/000-default.conf


# Start Apache
CMD ["apache2-foreground"]
