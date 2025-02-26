# Menggunakan base image PHP dengan Apache
FROM php:8.1-apache

# Install MySQL Client dan unzip
RUN apt-get update && apt-get install -y \
    imagemagick \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmagickwand-dev --no-install-recommends \
    libpng-dev \
    && rm -rf /var/lib/apt/lists/* \
    && a2enmod rewrite \
    && docker-php-ext-install exif \
    && docker-php-ext-configure gd --with-freetype --with-jpeg && docker-php-ext-install -j$(nproc) gd \
    && pecl install imagick && docker-php-ext-enable imagick \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install pdo pdo_mysql

# Salin project ke dalam container
COPY . /var/www/html

# Hapus file setup_completed.flag
RUN rm -f /var/www/html/setup_completed.flag

# Set hak akses untuk folder
RUN chown -R www-data:www-data /var/www/html

RUN a2enmod rewrite


# Port untuk Apache
EXPOSE 80

# Jalankan Apache ketika container dimulai
CMD ["apache2-foreground"]
