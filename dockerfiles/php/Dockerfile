ARG PHP_VERSION
FROM php:${PHP_VERSION}-fpm-alpine

ARG PHP_EXTENSIONS
ARG MORE_EXTENSION_INSTALLER
ARG ALPINE_REPOSITORIES
ARG COMPOSER_REPOSITORIES

ENV BOOT2DOCKER_ID 1000
ENV BOOT2DOCKER_GID 50

COPY php/extensions /tmp/extensions
WORKDIR /tmp/extensions

ENV EXTENSIONS=",${PHP_EXTENSIONS},"
ENV MC="-j$(nproc)"

RUN export MC="-j$(nproc)" \
    && chmod +x install.sh \
    && chmod +x "${MORE_EXTENSION_INSTALLER}" \
    && sh install.sh \
    && sh "${MORE_EXTENSION_INSTALLER}"

# Tweaks to give PHP write permissions to the app
RUN apk --no-cache add shadow
RUN groupadd -g 50 staff
RUN usermod -u ${BOOT2DOCKER_ID} www-data && \
    usermod -G staff www-data
RUN groupmod -g $(($BOOT2DOCKER_GID + 10000)) $(getent group $BOOT2DOCKER_GID | cut -d: -f1)
RUN groupmod -g ${BOOT2DOCKER_GID} staff

# Add composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# change composer image sources
USER 1000
RUN composer config -g repo.packagist composer ${COMPOSER_REPOSITORIES}
USER root
RUN composer config -g repo.packagist composer ${COMPOSER_REPOSITORIES}

WORKDIR /var/www/html

RUN rm -rf /tmp/*
