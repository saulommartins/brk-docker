#FROM php:7.1.15-fpm
#
#USER root
#
#run apt-get update && \
#apt-get install -yq \
#    libfreetype6-dev \
#    libmcrypt-dev \
#    libpng12-dev \
#    libjpeg-dev \
#    libpng-dev \
#    libgmp-dev && \
#apt-get install -y libpq-dev && \
#docker-php-ext-install pdo \
#    pdo_mysql \
#    mysqli \
#    gd \
#    mbstring \
#    mcrypt \
#    zip \
#    gmp && \
#pecl install xdebug-2.5.0 \
#	&& docker-php-ext-enable xdebug && \
#curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
#apt-get -y install vim && \
#apt-get -y install git
#
#WORKDIR /var/www


FROM ubuntu:12.04
MAINTAINER Alexander Schenkel <alex@alexi.ch>


RUN apt-get update && \
    apt-get install -y \
      apache2 \
      php5 \
      php5-cli \
      libapache2-mod-php5 \
      php5-gd \
      php5-ldap \
      php5-mysql \
      php5-pgsql \
      php5-curl \
      curl \
      libcurl3 \
      libcurl3-dev \
      php5-curl


COPY apache_default /etc/apache2/sites-available/default
COPY apache_default-ssl /etc/apache2/sites-available/default-ssl
COPY apache_default-zonaoeste /etc/apache2/sites-available/default-zonaoeste
COPY apache_default-ssl-zonaoeste /etc/apache2/sites-available/default-ssl-zonaoeste
COPY apache_default-saneaqua /etc/apache2/sites-available/default-saneaqua
COPY apache_default-ssl-saneaqua /etc/apache2/sites-available/default-ssl-saneaqua
COPY ports.conf /etc/apache2/ports.conf
COPY run /usr/local/bin/run
RUN chmod +x /usr/local/bin/run
RUN a2enmod rewrite
RUN mkdir /etc/apache2/ssl
COPY apache.crt /etc/apache2/ssl/apache.crt
COPY apache.key /etc/apache2/ssl/apache.key
#RUN make-ssl-cert generate-default-snakeoil --force-overwrite
RUN a2enmod ssl
RUN service apache2 restart
RUN a2ensite default-ssl
RUN a2ensite default-zonaoeste
RUN a2ensite default-ssl-zonaoeste
RUN a2ensite default-saneaqua
RUN a2ensite default-ssl-saneaqua


EXPOSE 80
EXPOSE 443
CMD ["/usr/local/bin/run"]

WORKDIR /var/www
