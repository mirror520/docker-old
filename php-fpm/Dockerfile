FROM php:fpm

RUN apt-get update \ 
 && apt-get upgrade -y \
 && apt-get install libxml2-dev -y \
 && apt-get install libldap2-dev -y \
 && apt-get install libfreetype6-dev libjpeg62-turbo-dev libpng-dev -y \
 && apt-get install wget -y

RUN docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \ 
 && docker-php-ext-configure gd --with-freetype-dir=/usr --with-jpeg-dir=/usr \
 && docker-php-ext-install pdo pdo_mysql soap ldap gd 

RUN mkdir /var/lib/browscap
RUN wget http://browscap.org/stream?q=PHP_BrowsCapINI -O /var/lib/browscap/browscap.ini
