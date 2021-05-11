FROM php:7.3.19-apache
LABEL version="1.0" maintainer="Pierre-Emmanuel POUPARDIN <ppoupardin@toshiba-teis.com>"
RUN apt-get update -y \
&& apt-get install -y \
        libzip-dev \
        zip \
        libpng-dev \
        libbz2-dev \
        libxml2-dev \
        libxslt-dev \
        libfreetype6-dev \
        libmcrypt-dev \
        libjpeg-dev \
        libmcrypt-dev \
        nano \
&& curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
&& docker-php-ext-install \
     bcmath \
     calendar \
     exif \
     gettext \
     sockets \
     mysqli \
     pdo_mysql \
     opcache \
     bz2 \
     soap \
     xsl \
&& docker-php-ext-configure gd \
    --with-freetype-dir=/usr/include/freetype2 \
    --with-png-dir=/usr/include \
    --with-jpeg-dir=/usr/include \
&& docker-php-ext-install gd \
&& a2enmod rewrite headers socache_shmcb ssl \
&& service apache2 restart
COPY conf/php.ini /usr/local/etc/php/conf.d/app.ini
COPY conf/vhost.conf /etc/apache2/sites-available/000-default.conf
RUN chown -R www-data:www-data /var/www/html \
&& service apache2 restart
