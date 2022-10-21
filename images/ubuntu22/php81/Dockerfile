# OS: Ubuntu 22.04
# PHP: 8.1
# Nodejs: 16

FROM ubuntu:22.04

# LTS 16
ARG NODE_VERSION=16

WORKDIR /var/www/html

ENV TZ=UTC
ENV LOCALE="LANG=C.UTF-8"

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update && apt-get upgrade -y \
    && apt-get install -y software-properties-common zip unzip git curl vim \
    && apt-get install -y php php-mysql php-gd php-zip php-mbstring php-pdo php-xml php-curl \
    && php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer

RUN curl -sL https://deb.nodesource.com/setup_$NODE_VERSION.x | bash - \
    && apt-get install -y nodejs \
    && npm install -g npm

RUN apt-get install -y apache2 apache2-utils

RUN apt-get install -y mysql-client

RUN apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN a2enmod rewrite

# 中文語系顯示
RUN echo $LOCALE >> /etc/profile

CMD ["apache2ctl", "-D", "FOREGROUND"]
EXPOSE 80

