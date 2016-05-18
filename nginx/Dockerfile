FROM debian:jessie

MAINTAINER Sulaeman <me@sulaeman.com>

ENV NPS_VERSION=1.11.33.2 \
    NGINX_VERSION=1.10.0 \
    NGINX_USER=www-data \
    NGINX_SITECONF_DIR=/etc/nginx/sites-available \
    NGINX_LOG_DIR=/var/log/nginx \
    NGINX_TEMP_DIR=/var/lib/nginx \
    NGINX_SETUP_DIR=/var/cache/nginx

RUN apt-get update \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y wget perl libssl1.0.0 libxslt1.1 libgd3 libxpm4 libgeoip1 libav-tools \
 && rm -rf /var/lib/apt/lists/*

COPY setup/ ${NGINX_SETUP_DIR}/
RUN bash ${NGINX_SETUP_DIR}/install.sh

ADD nginx.conf /etc/nginx/
ADD php-fpm.conf /etc/nginx/
ADD hhvm.conf /etc/nginx/
ADD default.conf /etc/nginx/sites-available/
ADD site.conf /etc/nginx/sites-available/

ADD conf.d/headers.conf /etc/nginx/conf.d/
ADD conf.d/pagespeed.conf /etc/nginx/conf.d/
ADD conf.d/spider.conf /etc/nginx/conf.d/

# ADD ssl/cert.pem /etc/nginx/ssl/
# ADD ssl/key.pem /etc/nginx/ssl/

RUN usermod -u 1000 www-data

CMD ["nginx"]

EXPOSE 80 443
