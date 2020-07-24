FROM ubuntu_base:latest

ENV PHP_VERSION 7.2

RUN set -ex \
    # 安装php
    && apt-get -y install \
        php$PHP_VERSION \
        php$PHP_VERSION-mysql \
        php$PHP_VERSION-redis \
        php$PHP_VERSION-fpm \
        php$PHP_VERSION-curl \
        php$PHP_VERSION-xml \
        php$PHP_VERSION-json \
        php$PHP_VERSION-gd \
        php$PHP_VERSION-mbstring \
        php$PHP_VERSION-gmp \
        php$PHP_VERSION-ldap \
        php$PHP_VERSION-zip \
    && apt-get clean

RUN set -ex \
    # Composer
    && wget https://install.phpcomposer.com/composer.phar -O /usr/local/bin/composer \
    && chmod +x /usr/local/bin/composer \
    && composer config -g repo.packagist composer https://packagist.phpcomposer.com

RUN set -ex \   
    && useradd www \
    && usermod -s /sbin/nologin www \
    && mkdir -p /data/logs/php \
    && mkdir -p /data/logs/php \
    && chmod -R 777 /data/logs/php

COPY opt /opt

RUN sed -i "s/PHP_VERSION/$PHP_VERSION/" /opt/conf/supervisor/conf.d/php-fpm.conf

EXPOSE 9000

