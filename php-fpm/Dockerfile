FROM letsdockerize/laradock-php-fpm:2.3-7.3

ADD ./laravel.ini /usr/local/etc/php/conf.d
ADD ./laravel.pool.conf /usr/local/etc/php-fpm.d/

RUN usermod -u 1000 www-data
RUN docker-php-ext-install bcmath

WORKDIR /var/www/laravel

CMD ["php-fpm"]

EXPOSE 9000
