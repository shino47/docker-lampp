FROM php:5.6-apache

RUN apt-get update \
  && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev libwebp-dev libxpm-dev \
  && docker-php-ext-configure gd \
    --with-freetype-dir=/usr \
    --with-jpeg-dir=/usr \
    --with-png-dir=/usr \
    --with-webp-dir=/usr \
    --with-xpm-dir=/usr \
  && docker-php-ext-install gd pdo_mysql \
  && a2enmod rewrite \
  && apt-get clean all

CMD ["apache2-foreground"]
