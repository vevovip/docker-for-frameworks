FROM php:7.4-fpm

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

RUN apt-get install -y supervisor
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/
RUN install-php-extensions amqp gd mcrypt xsl intl zip bz2 mbstring pdo_mysql pdo_pgsql mysqli bcmath xdebug sockets rdkafka

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

#RUN useradd -ms /bin/bash vevovip
#USER vevovip

WORKDIR /var/www
CMD ["php-fpm"]
EXPOSE 9000
