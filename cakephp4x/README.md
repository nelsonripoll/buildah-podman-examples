```
# buildah from --name cakephp4x php:8-fpm > /dev/null
# buildah images
# buildah run cakephp4x apt-get update -y > /dev/null
# buildah config --workingdir "/opt" cakephp4x
# buildah run cakephp4x curl -sS https://getcomposer.org/installer -o composer-setup.php
# buildah run cakephp4x php composer-setup.php --install-dir=/usr/local/bin --filename=composer
# buildah run cakephp4x rm composer-setup.php    
# buildah run cakephp4x apt-get install --yes libfreetype6-dev libjpeg62-turbo-dev libpng-dev libzip-dev libicu-dev git unzip > /dev/null
# buildah run cakephp4x docker-php-ext-configure gd --with-freetype --with-jpeg > /dev/null
# buildah run cakephp4x docker-php-ext-install -j$(nproc) intl pdo_mysql zip gd pcntl > /dev/null
```
