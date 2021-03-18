```
buildah from --name cakephp4x php:8-fpm
buildah images
buildah run cakephp4x apt-get update --yes
buildah config --workingdir "/opt" cakephp4x
buildah run cakephp4x curl -sS https://getcomposer.org/installer -o composer-setup.php
buildah run cakephp4x php composer-setup.php --install-dir=/usr/local/bin --filename=composer
buildah run cakephp4x rm composer-setup.php    
buildah run cakephp4x apt-get install --yes libfreetype6-dev libjpeg62-turbo-dev libpng-dev libzip-dev libicu-dev git unzip
buildah run cakephp4x docker-php-ext-configure gd --with-freetype --with-jpeg
buildah run cakephp4x docker-php-ext-install -j$(nproc) intl pdo_mysql zip gd pcntl
buildah run composer create-project --no-interaction --prefer-dist cakephp/app:~4.0 cakephp4x_app
buildah config --workingdir "/opt/cakephp4x_app" cakephp4x
buildah config --cmd php bin/cake.php server -H 0.0.0.0 -p 8080
```
