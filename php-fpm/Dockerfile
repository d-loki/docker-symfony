FROM alpine:3.13

RUN apk add --no-cache \
    coreutils \
    gettext \
    php7-fpm \
    php7-apcu \
    php7-ctype \
    php7-curl \
    php7-dom \
    php7-gd \
    php7-iconv \
    php7-imagick \
    php7-json \
    php7-intl \
    php7-mcrypt \
    php7-fileinfo\
    php7-mbstring \
    php7-opcache \
    php7-openssl \
    php7-pdo \
    php7-pdo_mysql \
    php7-mysqli \
    php7-xml \
    php7-zlib \
    php7-phar \
    php7-tokenizer \
    php7-session \
    php7-simplexml \
    php7-xdebug \
    php7-zip \
    php7-xmlwriter \
    make \
    curl

RUN curl -sS https://getcomposer.org/installer | tee composer-setup.php \
    && php7 composer-setup.php && rm composer-setup.php* \
    && chmod +x composer.phar && mv composer.phar /usr/bin/composer \
    && ln -s /usr/bin/php7 /usr/local/bin/php

ARG SYMFONY_CLI_VERSION
RUN wget https://github.com/symfony/cli/releases/download/v$SYMFONY_CLI_VERSION/symfony_linux_amd64.gz \
    && gzip -d symfony_linux_amd64.gz \
    && mv symfony_linux_amd64 symfony \
    && chmod +x symfony \
    && mv symfony /usr/local/bin/

RUN apk add --update nodejs npm \
    && npm install --global yarn

COPY symfony.ini /etc/php7/conf.d/
COPY symfony.ini /etc/php7/cli/conf.d/

COPY symfony.pool.conf /etc/php7/php-fpm.d/

WORKDIR /var/www/symfony

CMD ["php-fpm7", "-F"]

EXPOSE 9001
