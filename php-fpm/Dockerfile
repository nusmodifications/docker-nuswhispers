FROM laradock/php-fpm:2.6.1-7.4

ADD ./laravel.ini /usr/local/etc/php/conf.d
ADD ./laravel.pool.conf /usr/local/etc/php-fpm.d/

RUN usermod -u 1000 www-data
RUN docker-php-ext-install bcmath

WORKDIR /var/www/laravel

CMD ["php-fpm"]

EXPOSE 9000
