# OS: Ubuntu 20.04
# PHP: 8.1
# Nodejs: 16

FROM ubuntu:20.04

# LTS 16
ARG NODE_VERSION=16

WORKDIR /var/www/html

ENV TZ=UTC
ENV LOCALE="LANG=C.UTF-8"

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update && apt-get upgrade -y \
    && apt-get install -y software-properties-common zip unzip git curl zlibc vim \
    && add-apt-repository ppa:ondrej/php \
    && apt-get update \
    && apt-get install -y php8.1 php8.1-mysql php8.1-gd php8.1-zip php8.1-mbstring php8.1-pdo php8.1-xml php8.1-curl php8.1-ldap \
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

