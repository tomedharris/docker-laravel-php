FROM tharrisio/laravel-php:6-fpm

RUN pecl install xdebug-2.7.2 \
    && docker-php-ext-enable xdebug

# Use our custom xdebug config.
COPY conf.d/xdebug.ini /usr/local/etc/php/conf.d/

RUN echo "pm.status_path = /status" >> /usr/local/etc/php-fpm.d/www.conf
RUN echo "pm.max_children = 15" >> /usr/local/etc/php-fpm.d/www.conf

WORKDIR /app
