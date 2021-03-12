```
# buildah from --name cakephp4x php:8-fpm
Getting image source signatures
Copying blob d452cc5944b4 done  
Copying blob 45b42c59be33 done  
Copying blob 79a8e4ec25c6 done  
Copying blob b2615679786b done  
Copying blob 366d949cba16 done  
Copying blob 4c65628244f3 done  
Copying blob f6e171dee733 done  
Copying blob 4bd1ee75d9c6 done  
Copying blob 6457f412d96b done  
Copying blob db9025a44790 done  
Copying config 4ebd60322a done  
Writing manifest to image destination
Storing signatures

# buildah images
REPOSITORY              TAG     IMAGE ID       CREATED      SIZE
docker.io/library/php   8-fpm   4ebd60322a2b   6 days ago   415 MB

# buildah containers
CONTAINER ID  BUILDER  IMAGE ID     IMAGE NAME                       CONTAINER NAME
0ed6c59f47a1     *     4ebd60322a2b docker.io/library/php:8-fpm      cakephp4x

# buildah run cakephp4x apt-get update -y
Get:1 http://deb.debian.org/debian buster InRelease [122 kB]
Get:2 http://security.debian.org/debian-security buster/updates InRelease [65.4 kB]
Get:3 http://deb.debian.org/debian buster-updates InRelease [51.9 kB]
Get:4 http://security.debian.org/debian-security buster/updates/main amd64 Packages [268 kB]
Get:5 http://deb.debian.org/debian buster/main amd64 Packages [7907 kB]
Get:6 http://deb.debian.org/debian buster-updates/main amd64 Packages [9504 B]
Fetched 8423 kB in 2s (3764 kB/s)
Reading package lists... Done

# buildah config --workingdir "/opt" cakephp4x

# buildah run cakephp4x curl -sS https://getcomposer.org/installer -o composer-setup.php

# buildah run cakephp4x php composer-setup.php --install-dir=/usr/local/bin --filename=composer
All settings correct for using Composer
Downloading...

Composer (version 2.0.11) successfully installed to: /usr/local/bin/composer
Use it: php /usr/local/bin/composer

# buildah run cakephp4x rm composer-setup.php    

# buildah run cakephp4x php -m
buildah run cakephp4x php -m
[PHP Modules]
Core
ctype
curl
date
dom
fileinfo
filter
ftp
hash
iconv
json
libxml
mbstring
mysqlnd
openssl
pcre
PDO
pdo_sqlite
Phar
posix
readline
Reflection
session
SimpleXML
sodium
SPL
sqlite3
standard
tokenizer
xml
xmlreader
xmlwriter
zlib

# buildah run cakephp4x apt-get install --yes libfreetype6-dev libjpeg62-turbo-dev libpng-dev libzip-dev libicu-dev git unzip > /dev/null

# buildah run cakephp4x docker-php-ext-configure gd --with-freetype --with-jpeg > /dev/null

# buildah run cakephp4x docker-php-ext-install -j$(nproc) intl pdo_mysql zip gd pcntl > /dev/null
```
