FROM gitpod/workspace-full

ARG DEBIAN_FRONTEND=noninteractive

ENV DOCKER 1

ENV PHP_OPCACHE_ENABLE "on"
ENV PHP_DISPLAY_ERRORS "off"
ENV PHP_ERROR_REPORTING "4983"

# Install packages
USER root
RUN mkdir -p /etc/apt/sources.list.d/ \
 && echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu bionic main" > /etc/apt/sources.list.d/ondrej-ubuntu-php-bionic.list \
 && apt-get update \
 && apt-get install -y supervisor \
    nginx \
    php7.4-fpm php-apcu php7.4-curl php7.4-gd php-imagick php7.4-intl php7.4-json php7.4-mbstring php-mongodb php7.4-mysql php-oauth php-sodium php7.4-tidy php7.4-xml php-yaml php7.4-zip \
 && curl --silent --show-error https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Create required directories and set file permissions
RUN mkdir -p /var/run/php

# Configure the services
COPY ./docker/supervisord /etc/supervisor/conf.d/
COPY ./docker/php/fpm.conf /etc/php/7.4/fpm/php-fpm.conf
COPY ./docker/nginx/default.conf /etc/nginx/sites-available/default
