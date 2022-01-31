FROM php:8.1-apache

RUN apt-get update \
  && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev libwebp-dev libxpm-dev \
  && docker-php-ext-configure gd \
    --with-freetype \
    --with-jpeg \
    --with-webp \
    --with-xpm \
  && docker-php-ext-install gd pdo_mysql opcache \
  && a2enmod rewrite \
  && apt-get clean

COPY conf.ini "$PHP_INI_DIR/conf.d/"

CMD ["apache2-foreground"]
