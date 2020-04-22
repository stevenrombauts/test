FROM gitpod/workspace-mysql

ARG DEBIAN_FRONTEND=noninteractive

ENV DOCKER 1

ENV PHP_OPCACHE_ENABLE "on"
ENV PHP_DISPLAY_ERRORS "off"
ENV PHP_ERROR_REPORTING "4983"

# Install packages
USER root
RUN apt-get update \
 && apt-get install -y supervisor \
 && nginx \
 && php7.4-fpm \
 && curl --silent --show-error https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Configure the services
COPY ./docker/supervisord /etc/supervisor/conf.d/
COPY ./docker/php/fpm.conf /etc/php/7.4/fpm/php-fpm.conf
COPY ./docker/nginx/default.conf /etc/nginx/sites-available/default

# Create required directories and set file permissions
RUN mkdir -p /var/run/php \
 && chown -R gitpod:gitpod /var/run/php /etc/php /etc/nginx /etc/supervisor
