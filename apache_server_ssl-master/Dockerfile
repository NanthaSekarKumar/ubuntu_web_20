FROM ubuntu:20.04
MAINTAINER darkprime <nanthacollege17@gmail.com>

ENV APACHE_HTTP_PROTOCOLS http/2
ENV APACHE_CONFDIR=/etc/apache2
ENV APACHE_SERVER_NAME localhost
ENV PHP_TIMEZONE=Europe/Rome
ENV APACHE_DOC_ROOT=/var/www/html
ENV XDEBUG_ENABLE=0
ENV PHP_VERSION=8.2.40
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_LOG_DIR /var/log/apache2
ENV LANG C

RUN apt-get update && \
    apt-get install -y software-properties-common && \
    rm -rf /var/lib/apt/lists/* &&\
    LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php 
RUN apt-get update
RUN apt-get install apt-utils -y
RUN apt-get install apache2 -y
RUN mkdir -p /var/lock/apache2
RUN mkdir -p /var/run/apache2
RUN apt-get install -y php8.0 libapache2-mod-php8.0 php8.0-cgi php8.0-cli php8.0-curl php8.0-imap php8.0-gd php8.0-mysql php8.0-pgsql php8.0-sqlite3 php8.0-mbstring php8.0-bz2 php8.0-mcrypt php8.0-xmlrpc php8.0-gmp php8.0-xsl php8.0-soap php8.0-xml php8.0-zip php8.0-dba php8.0-phpdbg php8.0-fpm php8.0-cli php8.0-cgi libphp8.0-embed libapache2-mod-php8.0 php8.0-fpm libapache2-mod-fcgid -y

COPY apache2.conf /etc/apache2/apache2.conf
COPY dir.conf /etc/apache2/mods-available/dir.conf

RUN a2enmod rewrite
RUN a2enmod headers
RUN a2enmod ssl
RUN a2enmod proxy_fcgi setenvif
RUN a2enconf php8.0-fpm
RUN a2enconf php8.0-cgi
RUN a2dissite 000-default.conf
RUN a2ensite default-ssl.conf

EXPOSE 443

CMD ["apache2ctl", "-D", "FOREGROUND"]