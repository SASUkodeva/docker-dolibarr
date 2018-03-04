FROM php:5.6-apache

RUN apt-get update && apt-get install -y libpng12-dev libjpeg-dev libldap2-dev \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr 

RUN docker-php-ext-install gd
RUN docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/
RUN docker-php-ext-install ldap
RUN docker-php-ext-install mysqli
RUN apt-get purge -y libpng12-dev libjpeg-dev libldap2-dev

ENV DOLI_VER 7.0.0
		
RUN cd /tmp 
RUN curl -L "https://github.com/dolibarr/dolibarr/archive/${DOLI_VER}.tar.gz" -o dolibarr.tar.gz  \
	&& tar -xzf dolibarr.tar.gz \
	&& cp -R dolibarr-${DOLI_VER}/htdocs/. /var/www/html \
	&& rm -R dolibarr-${DOLI_VER} \
	&& rm dolibarr.tar.gz

RUN mkdir /var/www/html/documents \
    && chown -hR www-data:www-data /var/www/html

COPY php.ini /usr/local/etc/php

VOLUME ["/var/www/html/conf", "/var/www/html/documents"]

EXPOSE 80