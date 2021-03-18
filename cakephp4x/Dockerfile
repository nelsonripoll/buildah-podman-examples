# https://hub.docker.com/_/php
FROM php:8-fpm
ENV APPNAME=cakephp4x_app
WORKDIR /opt

# UPDATE IMAGE
RUN apt-get update

# INSTALL COMPOSER
RUN EXPECTED_SIGNATURE="$(curl https://composer.github.io/installer.sig)" \
 && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
 && ACTUAL_SIGNATURE="$(php -r "echo hash_file('sha384', 'composer-setup.php');")" \
 && if [ "$EXPECTED_SIGNATURE" != "$ACTUAL_SIGNATURE" ]; then >&2 echo 'ERROR: Invalid installer signature'; exit 1; fi \
 && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
 && rm composer-setup.php

# INSTALL & CONFIGURE CAKEPHP DEPENDENCIES
RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev libzip-dev libicu-dev git unzip \
 && docker-php-ext-configure gd --with-freetype --with-jpeg \
 && docker-php-ext-install -j$(nproc) intl pdo_mysql zip gd pcntl

RUN composer create-project --no-interaction --prefer-dist cakephp/app:~4.0 $APPNAME

WORKDIR /opt/$APPNAME

CMD ["php", "bin/cake.php", "server", "-H", "0.0.0.0", "-p", "8080"]
