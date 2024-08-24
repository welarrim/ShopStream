# Use the official PHP 8.3 FPM image as the base image
FROM php:8.3-fpm

# Arguments for UID and GID
ARG USER_ID
ARG GROUP_ID

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    libzip-dev \
    curl \
    && docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd zip \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Create a user with the same UID and GID as the host user
RUN groupadd -g ${GROUP_ID} appuser && \
    useradd -u ${USER_ID} -g appuser -m appuser

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Set the working directory
WORKDIR /var/www/html

# Switch to the newly created user
USER appuser

# Expose port 9000 and start the PHP-FPM service
EXPOSE 9000

CMD ["php-fpm"]