FROM php:8.1-fpm as base
LABEL name=bedrock
LABEL intermediate=true

# Install essential packages
RUN apt-get update \
  && apt-get install -y \
    build-essential \
    curl \
    git \
    gnupg \
    less \
    nano \
    vim \
    unzip \
    zip \
  && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
  && rm -rf /var/lib/apt/lists/* \
  && apt-get clean

FROM base as php
LABEL name=bedrock
LABEL intermediate=true

# Install php extensions and related packages
ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/
RUN chmod +x /usr/local/bin/install-php-extensions && sync \
  && install-php-extensions \
    @composer \
    exif \
    gd \ 
    memcached \
    mysqli \
    pcntl \
    pdo_mysql \
    zip \
  && apt-get update \
  && apt-get install -y \
    gifsicle \
    jpegoptim \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libmemcached-dev \
    locales \
    lua-zlib-dev \
    optipng \
    pngquant \
  && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
  && rm -rf /var/lib/apt/lists/* \
  && apt-get clean

FROM php as bedrock
LABEL name=bedrock

# Install nginx & supervisor
RUN curl -sL https://deb.nodesource.com/setup_16.x | bash \
  && apt-get update \
  && apt-get install -y \
    nginx \
    nodejs \
    supervisor \
  && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
  && rm -rf /var/lib/apt/lists/* \
  && apt-get clean \
  && npm install -g yarn

# Configure nginx, php-fpm and supervisor
COPY ./nginx/nginx.conf /etc/nginx/nginx.conf
COPY ./nginx/sites-enabled /etc/nginx/conf.d
COPY ./nginx/sites-enabled /etc/nginx/sites-enabled
COPY ./www.conf /etc/php/8.1/fpm/pool.d/www.conf
COPY ./supervisord.conf /etc/supervisord.conf

CMD ["/usr/bin/supervisord -c /etc/supervisord.conf"]
