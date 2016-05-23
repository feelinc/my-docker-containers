FROM debian:jessie

MAINTAINER Sulaeman <me@sulaeman.com>

RUN apt-get update \
  && apt-get install -y \
    cron \
    libmagickwand-dev

# Add the necessary keys
RUN apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0x5a16e7281be7a449

# Add to repository sources list
RUN echo deb http://dl.hhvm.com/debian jessie main | tee /etc/apt/sources.list.d/hhvm.list

# Update cache and install
RUN apt-get update && apt-get -y install \
    hhvm \
    supervisor

# Install Composer and make it available in the PATH
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer

ADD ./config.hdf /etc/hhvm/
ADD ./php.ini /etc/hhvm/
ADD ./server.ini /etc/hhvm/
ADD ./supervisor-hhvm.conf /etc/supervisor/conf.d/

RUN usermod -u 1000 www-data

RUN chown www-data:1000 /var/run/hhvm

WORKDIR /var/www

CMD ["supervisord", "-n"]

EXPOSE 9001
