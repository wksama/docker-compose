ARG PHP_VERSION
FROM php:${PHP_VERSION}-fpm-alpine

ARG PHP_EXTENSIONS
ARG MORE_EXTENSION_INSTALLER
ARG ALPINE_REPOSITORIES

COPY php/extensions /tmp/extensions
WORKDIR /tmp/extensions

ENV EXTENSIONS=",${PHP_EXTENSIONS},"
ENV MC="-j$(nproc)"

RUN export MC="-j$(nproc)" \
    && chmod +x install.sh \
    && chmod +x "${MORE_EXTENSION_INSTALLER}" \
    && sh install.sh \
    && sh "${MORE_EXTENSION_INSTALLER}"

# Add composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# change composer image sources
USER www-data
RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
USER root
RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

# Configure /app folder with sample app
RUN mkdir -p /app && rm -fr /var/www/html && ln -s /app /var/www/html

WORKDIR /app

RUN rm -rf /tmp/*
