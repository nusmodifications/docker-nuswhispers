FROM nginx:latest

COPY nginx.conf /etc/nginx/nginx.conf
COPY php-fpm.conf /etc/nginx/php-fpm.conf

COPY default.conf /etc/nginx/conf.d/default.conf

RUN usermod -u 1000 www-data

CMD ["nginx"]

EXPOSE 80
