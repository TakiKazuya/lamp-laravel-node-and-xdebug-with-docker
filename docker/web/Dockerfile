# 適宜必要なバージョンに変更してください。
FROM php:7.3-apache

# 必要なパッケージをインストール
RUN apt-get update \
    && apt-get install -y git zip unzip libzip-dev

COPY php-base.ini $PHP_INI_DIR/conf.d/

COPY httpd-base.conf /etc/apache2/sites-available/laravel.conf
RUN a2dissite 000-default.conf && a2ensite laravel.conf && a2enmod rewrite

# composer
RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

# node
RUN apt-get install -y nodejs npm && npm install n -g && n 14.15.3

# xdebug
RUN pecl install xdebug && docker-php-ext-enable xdebug

# その他拡張パッケージをインストール(必要なければ消してください)
RUN apt-get update \
    && apt-get install -y zlib1g-dev vim libpq-dev libicu-dev libfreetype6-dev libjpeg62-turbo-dev libpng-dev

RUN docker-php-ext-install pdo_mysql intl gd zip \
    && docker-php-ext-configure gd
