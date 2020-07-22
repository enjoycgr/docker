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
    && apt-get clean

RUN sed -i 's/;daemonize = yes/daemonize = no/' /etc/php/$PHP_VERSION/fpm/php-fpm.conf

COPY opt /opt

EXPOSE 9000

