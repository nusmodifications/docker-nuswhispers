FROM nginx:latest

COPY nginx.conf /etc/nginx/nginx.conf
COPY hhvm.conf /etc/nginx/hhvm.conf

COPY default.conf /etc/nginx/conf.d/default.conf

RUN usermod -u 1000 www-data

CMD ["nginx"]

EXPOSE 80
