FROM debian:jessie

# Install php7-cgi
RUN apt-get update \
 && apt-get install -y curl apt-transport-https lsb-release ca-certificates \
 && curl -sS https://packages.sury.org/php/apt.gpg > /etc/apt/trusted.gpg.d/php.gpg \
 && echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list \
 && apt-get update \
 && apt-get install -y php7.1-cgi php7.1-dev php-pear \
 && rm -rf /var/lib/apt/lists/*

# Install event pecl extension
RUN apt-get update\
 && apt-get install -y libevent-dev libssl-dev \
 && printf 'no\nyes\n/usr\no\nyes\nno' | pecl install event \
 && echo "extension=event.so" > /etc/php/7.1/mods-available/event.ini \
 && ln -s /etc/php/7.1/mods-available/event.ini /etc/php/7.1/cli/conf.d/20-event.ini \
 && ln -s /etc/php/7.1/mods-available/event.ini /etc/php/7.1/cgi/conf.d/20-event.ini \
 && rm -rf /var/lib/apt/lists/* \
 && php -i | grep event
