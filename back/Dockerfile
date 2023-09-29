FROM php:8.2-cli

RUN apt-get update \
    &&  apt-get install -y --no-install-recommends \
        locales apt-utils git libicu-dev g++ libpng-dev libxml2-dev libzip-dev libonig-dev libxslt-dev unzip libpq-dev nodejs npm wget \
        apt-transport-https lsb-release ca-certificates

RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen  \
    &&  echo "fr_FR.UTF-8 UTF-8" >> /etc/locale.gen \
    &&  locale-gen

RUN curl -sS https://getcomposer.org/installer | php -- \
    &&  mv composer.phar /usr/local/bin/composer

RUN composer self-update 2.6.3

RUN curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.deb.sh' | bash

RUN apt install symfony-cli=5.5.10

RUN docker-php-ext-configure \
            intl \
    &&  docker-php-ext-install \
            pdo pdo_mysql pdo_pgsql opcache intl zip calendar dom mbstring gd xsl

RUN pecl install apcu grpc && docker-php-ext-enable apcu grpc

RUN npm install --global yarn

CMD tail -f /dev/null

RUN adduser symfony
RUN chown symfony:symfony /var/www/html
WORKDIR  /var/www/html/
#RUN chown jeremy:jeremy -R .

ENV TZ=UTC
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN printf '[PHP]\ndate.timezone = "UTC"\n' > /usr/local/etc/php/conf.d/tzone.ini
USER symfony


RUN git config --global user.email "tuto@gmail.com" \
    &&  git config --global user.name "Exemple" \
    &&  git config --global credential.helper store

COPY --chown=symfony:symfony . .
EXPOSE 8000