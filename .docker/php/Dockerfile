FROM php:7.4-fpm

MAINTAINER Anton Kuznetsov <ajusmith@gmail.com>

# +------+
# | INIT |
# +------+

# Import variables from docker-compose file
ARG PROJECT_NAME
ARG PROJECT_DOMEN

# install some bare necessities
RUN apt-get update && apt-get install -y \
    libssl-dev \
    libmcrypt-dev \
    libjpeg-dev \
    libpng-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpq-dev \
    zlib1g-dev \
    libicu-dev \
    libxslt-dev \
    zlib1g-dev \
    libzip-dev \
    zip \
    curl \
    ssh \
    vim \
    mc \
# git & unzip needed for composer
    unzip \
    git \
    openssl \
    g++ \
#ssmtp \
    --no-install-recommends \
    && rm -r /var/lib/apt/lists/*

# configure libraries
RUN docker-php-ext-configure gd --with-jpeg --with-freetype \
    && docker-php-ext-configure intl \
    && docker-php-ext-configure hash --with-mhash

# install required extensions
RUN docker-php-ext-install \
    -j$(nproc) gd \
    exif \
    intl \
    pdo_mysql \
    json \
    iconv \
    bcmath \
    zip \
    soap

# install crontab
RUN apt-get update && apt-get -y install cron

# Set timezone
ENV TZ Europe/Moscow
RUN echo $TZ > /etc/timezone && \
    apt-get update && apt-get install -y tzdata && \
    rm /etc/localtime && \
    ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata && \
    apt-get clean

# add XDebug for the dev env build
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

# +-----------+
# | CONFIGURE |
# +-----------+

# expose the xdebug port on dev build
ENV XDEBUG_EXPOSE_PORT ${XDEBUG_PORT:-9000}
EXPOSE $XDEBUG_EXPOSE_PORT

# configure app folder
WORKDIR /var/www/${PROJECT_DOMEN}/

# install npm
RUN curl -sL https://deb.nodesource.com/setup_13.x | bash -
RUN apt-get install -y nodejs
RUN npm install

# Install Composer
RUN curl -s http://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

RUN usermod -u 1000 www-data \
    && groupmod -g 1000 www-data

VOLUME "/usr/local/etc/php/conf.d"
