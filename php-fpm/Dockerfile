ARG PHP_VERSION

FROM php:${PHP_VERSION}-fpm

MAINTAINER Roman Akhmetyanov <vevogm@gmail.com>

# Additional tools
RUN apt-get update \
 && apt-get install -y --no-install-recommends \
    curl \
    nano \
    mc \
    vim \
    git \
    cron

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/
RUN install-php-extensions amqp gd mcrypt xsl intl zip bz2 pdo_mysql pdo_pgsql mysqli bcmath xdebug sockets memcached igbinary imagick mongodb rdkafka redis

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer \
 && chmod 755 /usr/bin/composer

RUN docker-php-ext-configure opcache --enable-opcache \
    && docker-php-ext-install opcache
# Copy opcache configration
COPY opcache.ini /usr/local/etc/php/conf.d/opcache.ini

# Enable XDebug
ADD xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

# Clear package lists
RUN rm -rf /var/lib/apt/lists/*
RUN sed -i '1i openssl_conf = default_conf' /etc/ssl/openssl.cnf && echo "\n[ default_conf ]\nssl_conf = ssl_sect\n[ssl_sect]\nsystem_default = system_default_sect\n[system_default_sect]\nMinProtocol = TLSv1.2\nCipherString = DEFAULT:@SECLEVEL=1" >> /etc/ssl/openssl.cnf

#RUN useradd -ms /bin/bash vevovip
#USER vevovip

WORKDIR /var/www
CMD ["php-fpm"]
EXPOSE 9000