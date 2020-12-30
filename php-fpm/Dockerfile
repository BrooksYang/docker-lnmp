#
#--------------------------------------------------------------------------
# Image Setup
#--------------------------------------------------------------------------
#
# Note: Base Image name format {image-tag}-{php-version}
#

ARG PHP_VERSION
FROM php:${PHP_VERSION}-fpm

MAINTAINER Brooks <brooksycq@gmail.com>

ARG PHP_VERSION

# always run apt update when start and after add new source list, then clean up at end.
RUN apt-get update -yqq \
    && pecl channel-update pecl.php.net \
    && apt-get install -y apt-utils openssl libssl-dev git libzip-dev zip unzip inetutils-ping \
    && docker-php-ext-configure zip \
    # Install extensions
    && docker-php-ext-install zip mysqli pdo_mysql bcmath pcntl tokenizer \
    # Install composer
    && curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/bin/composer

# Install gd iconv extension
RUN apt-get update \
    && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-install -j$(nproc) gd

# Install redis extension
RUN pecl install redis \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable redis

# Install imagick
RUN apt-get install -y libmagickwand-dev imagemagick \
    && pecl install imagick \
    && docker-php-ext-enable imagick

# Install opcache
# RUN docker-php-ext-install opcache

# Install swoole
# RUN pecl install swoole && docker-php-ext-enable swoole

# Install supervisor
RUN apt-get update \
     && apt-get install -y supervisor \
     && touch /var/run/supervisor.sock \
     && chmod 777 /var/run/supervisor.sock \
     && unlink /var/run/supervisor.sock

# Install Node
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - \
    && apt-get install -y nodejs

# Clean up
RUN apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && rm /var/log/lastlog /var/log/faillog

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000
