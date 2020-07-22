FROM ubuntu:18.04

# 设置源
RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak
COPY ./opt/sources/sources.list /etc/apt/sources.list

RUN set -ex \
    # 设置时区
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    # 更新
    && apt-get update -y \
    && apt-get upgrade -y \
    # 安装软件
    && apt-get -y install curl git wget unzip vim apt-utils supervisor \
    && apt-get clean

# 配置SSH
COPY ./opt/ssh /root/.ssh
RUN set -ex \
    && chmod 600 /root/.ssh/* \
    && ssh-keyscan -t rsa git.xiaoyinka.vip >> /root/.ssh/known_hosts \
    && ssh-keyscan -t rsa github.com >> /root/.ssh/known_hosts 

# root密码
RUN set -ex \
    && echo 'root:letmein111' | chpasswd   

COPY ./opt/conf /opt/conf

CMD ["supervisord", "-c", "/opt/conf/supervisor/supervisor.conf"] 
