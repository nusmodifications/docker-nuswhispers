FROM laradock/php-fpm:2.2-7.2

ADD ./laravel.ini /usr/local/etc/php/conf.d
ADD ./laravel.pool.conf /usr/local/etc/php-fpm.d/

RUN usermod -u 1000 www-data

WORKDIR /var/www/laravel

CMD ["php-fpm"]

EXPOSE 9000
