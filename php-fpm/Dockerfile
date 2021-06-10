FROM php:7.4-fpm

ENV TZ=Asia/Shanghai

COPY ./sources.list /etc/apt/sources.list

RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -

RUN apt-get update && apt-get install -y -f --allow-downgrades \
	sudo \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        git \
        zip \
        zlib1g-dev \
        supervisor \
	net-tools \
        procps \
	net-tools \
	supervisor \
	curl \
        sudo \
	wget \
        nodejs \
	libzip-dev
 
RUN  docker-php-ext-install -j$(nproc) iconv mysqli pdo_mysql zip pcntl bcmath

RUN  docker-php-ext-configure gd --with-freetype --with-jpeg

RUN docker-php-ext-install -j$(nproc) gd

RUN pecl install -o -f mcrypt && \
docker-php-ext-enable mcrypt

RUN pecl install -o -f redis \
&&  rm -rf /tmp/pear \
&&  docker-php-ext-enable redis

RUN wget https://mirrors.aliyun.com/composer/composer.phar -O /usr/bin/composer
RUN chmod +x /usr/bin/composer

COPY ./php.ini /usr/local/etc/php/conf.d/zz-php.ini
COPY ./php-fpm.conf /usr/local/etc/php-fpm.d/zz-php-fpm.conf
COPY ./opcache.ini /usr/local/etc/php/conf.d/opcache.ini
