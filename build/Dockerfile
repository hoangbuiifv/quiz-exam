FROM php:7.4.1-apache
RUN apt-get update && apt-get -y upgrade
# Get latest Composer
# COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
# Create system user to run Composer and Artisan Commands
RUN useradd -G www-data,root -u 1001 -d /home/sokanet sokanet
RUN mkdir -p /home/$user/.composer && \
    chown -R $user:$user /home/$user
RUN apt-get install -y zlib1g-dev
RUN apt-get install -y libzip-dev
RUN docker-php-ext-install pdo_mysql mysqli bcmath zip
COPY vhost.conf /etc/apache2/sites-available/000-default.conf
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN chown -R www-data:www-data /var/www/html && a2enmod rewrite

CMD ["apache2-foreground"]