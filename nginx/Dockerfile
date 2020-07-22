FROM ubuntu_base:latest

ENV NGINX_VERSION 1.16.1

RUN set -ex \
    # 安装依赖
    && apt-get -y install build-essential libtool \
                      zlib1g-dev openssl libssl-dev libpcre3 libpcre3-dev \
    # 下载源码
    && mkdir -p /opt/src \
    && cd /opt/src \
    && wget http://mirrors.sohu.com/nginx/nginx-$NGINX_VERSION.tar.gz \
    && tar zxvf nginx-$NGINX_VERSION.tar.gz \
    # 编译安装
    && useradd www \
    && usermod -s /sbin/nologin www \
    && cd /opt/src/nginx-$NGINX_VERSION \
    && ./configure \
        --prefix=/opt/nginx \
        --with-http_ssl_module \
        --with-pcre \
        --with-http_v2_module \
    && make \
    && make install \
    # 删除临时文件
    && apt-get clean \
    && rm -rf /opt/src

RUN set -ex \   
    && mkdir -p /data/logs/nginx/api \
    && mkdir -p /data/logs/nginx/xiaoyinka \
    && chmod -R 777 /data/logs/nginx

COPY opt /opt


