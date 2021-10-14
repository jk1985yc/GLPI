FROM php:7.3.25-fpm
#FROM php:5.6.34-fpm
#FROM php:5.6.31-fpm-alpine

#Set unicode
ENV LANG C.UTF-8

#install mcrypt、mysql Module
RUN apt-get update && apt-get install -y \
        git zip unzip \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        cron vim \
        libxslt-dev \
        libbz2-dev \
    && docker-php-ext-install mysqli sysvsem \
    && docker-php-ext-install bz2 calendar exif gettext pcntl pdo_mysql shmop sockets sysvmsg sysvshm wddx xsl
  # Install gd PHP extension.
RUN docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd
  # Install Zend OPcache PHP extension.
RUN docker-php-ext-install opcache
  # Install xmlrpc PHP extension.
RUN docker-php-ext-install -j$(nproc) xmlrpc
  # Install APCU PHP extension.
RUN pecl install apcu \
    && docker-php-ext-enable apcu \
    && echo "apc.enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-apcu.ini
  # Install intl PHP extension.
RUN apt-get install --assume-yes --no-install-recommends --quiet libicu-dev \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl
  # Install ldap PHP extension.
RUN apt-get install --assume-yes --no-install-recommends --quiet libldap2-dev \
    && docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
    && docker-php-ext-install ldap
  # Install soap PHP extension (required for some plugins).
RUN apt-get install --assume-yes --no-install-recommends --quiet libxml2-dev \
    && docker-php-ext-install soap
  # Install zip PHP extension.
RUN apt-get install --assume-yes --no-install-recommends --quiet libzip-dev \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip
  # Install cron service.
RUN apt-get install --assume-yes --no-install-recommends --quiet cron
  # Install acl to manage acl of writable directories.
RUN apt-get install --assume-yes --no-install-recommends --quiet acl
    
#install redis Module
RUN pecl install redis && docker-php-ext-enable redis

# 安裝環境、安裝工具
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

#enable funsioninventory cron job
COPY ./cron/root /var/spool/cron/crontabs/root

#Time
ENV TW=Asia/Taipei
RUN ln -snf /usr/share/zoneinfo/$TW /etc/localtime && echo $TW > /etc/timezone  

RUN mkdir /logs

COPY ./entrypoint.sh /entrypoint.sh
RUN chmod 777 /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
