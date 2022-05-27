FROM ubuntu:18.04

ARG DEBIAN_FRONTEND=noninteractive

RUN apt -y update

RUN apt install -y make build-essential checkinstall zlib1g-dev

RUN apt install -y build-essential automake autoconf make bzip2 libapr1-dev \

libaprutil1-dev libbrotli-dev libcurl4-openssl-dev libjansson-dev liblua5.2-dev \

libnghttp2-dev libpcre3-dev libssl-dev libxml2-dev wget zlib1g-dev \

libsqlite3-dev libbz2-dev libpng-dev libfreetype6-dev libgmp-dev libonig-dev libpspell-dev php-pspell  aspell-en \

libtidy-dev libxslt-dev php-dev libxml2-dev openssl 

RUN mkdir /opt/php7

RUN mkdir /opt/apache2

WORKDIR /tmp/apache2

COPY httpd-2.4.53.tar.gz .

RUN tar xvf httpd-2.4.53.tar.gz

WORKDIR /tmp/apache2/httpd-2.4.53

RUN ./configure --prefix=/opt/apache2 --enable-so

RUN make && make install

WORKDIR /tmp/php7

COPY php-7.4.29.tar.gz .

RUN tar xvf php-7.4.29.tar.gz

WORKDIR /tmp/php7/php-7.4.29

RUN ./configure \
--prefix=/opt/php7 \
--with-config-file-path=/opt/php7/etc \ 
--with-layout=PHP \
--with-pear \
--with-apxs2=/opt/apache2/bin/apxs \
--enable-calendar \
--enable-bcmath \
--with-gmp \
--enable-exif \
--with-openssl \
--with-mcrypt \
--with-mhash \
--with-zlib \
--with-bz2 \
--enable-zip \
--enable-ftp \
--enable-mbstring \
--with-iconv \
--enable-intl \
--with-icu-dir=/usr \
--with-gettext \
--with-pspell \
--enable-sockets \
--with-curl \
--with-curlwrappers \
--enable-gd \
--enable-gd-native-ttf \
--with-libdir=lib64 \
--with-jpeg-dir=/usr \
--with-png-dir=/usr \
--with-zlib-dir=/usr \
--with-xpm-dir=/usr \
--with-vpx-dir=/usr \
--with-freetype \
--with-t1lib=/usr \
--with-libxml-dir=/usr \
--with-mysql=mysqlnd \
--with-mysqli=mysqlnd \
--with-pdo-mysql=mysqlnd \
--with-config-file-path=/etc \
--enable-exif \
--enable-shmop \
--enable-wddx \
--enable-soap \
--with-xmlrpc \
--with-xsl \
--with-tidy=/usr \
--with-readline \
--enable-pcntl \
--enable-sysvshm \
--enable-sysvmsg \
--enable-shmop

RUN make && make install

RUN apt install -y libapache2-mod-php

CMD ["/opt/apache2/bin/apachectl", "-D", "FOREGROUND"]
