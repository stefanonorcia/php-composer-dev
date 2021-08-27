FROM ubuntu:20.04
MAINTAINER Stefano Norcia <stefano.norcia@gmail.com>
LABEL Description="Ubuntu HTTPD" \
      License="Apache License 2.0" \
      Usage="docker build -t httpd ." \
      Version="0.1"

ARG URL=example.com

ENV TZ=Europe/Berlin\
    DEBIAN_FRONTEND=noninteractive \
    URL=$URL

# aggiornamento delle dipendenze
RUN apt-get update
# installazione tramite apt-get di apache 2
RUN apt-get install -y \
            	nano \
            	apache2 \
            	libapache2-mod-php \
            	php \
            	php-cli \
            	php-common \
            	php-curl \
            	php-dev \
            	php-fpm \
            	php-gd \
            	php-xdebug \
            	php-tidy \
            	php-json \
            	php-mbstring \
            	php-mysql \
            	php-zip \
                php-bcmath \
            	composer \
                curl \

#APACHE2 CONF
RUN touch /etc/apache2/sites-available/$URL.conf
RUN echo "<VirtualHost *:443>" >> /etc/apache2/sites-available/$URL.conf
RUN echo "ServerName $URL" >> /etc/apache2/sites-available/$URL.conf
RUN echo "ServerAdmin webmaster@localhost" >> /etc/apache2/sites-available/$URL.conf
RUN echo "DocumentRoot /var/www/$URL" >> /etc/apache2/sites-available/$URL.conf
RUN echo "SSLEngine on" >> /etc/apache2/sites-available/$URL.conf
RUN echo "SSLCertificateFile /etc/apache2/ssl/crt" >> /etc/apache2/sites-available/$URL.conf
RUN echo "SSLCertificateKeyFile /etc/apache2/ssl/key" >> /etc/apache2/sites-available/$URL.conf
RUN echo "ErrorLog \${APACHE_LOG_DIR}/cp_error.log" >> /etc/apache2/sites-available/$URL.conf
RUN echo "CustomLog \${APACHE_LOG_DIR}/cp_access.log combined" >> /etc/apache2/sites-available/$URL.conf
RUN echo "</VirtualHost>" >> /etc/apache2/sites-available/$URL.conf

#XDEBUG
RUN echo "xdebug.remote_enable = 1" >> /etc/php/7.4/mods-available/xdebug.ini
RUN echo "xdebug.remote_host = host.docker.internal" >> /etc/php/7.4/mods-available/xdebug.ini
RUN echo "xdebug.remote_port = 9000" >> /etc/php/7.4/mods-available/xdebug.ini
RUN echo "xdebug.remote_autostart = 1" >> /etc/php/7.4/mods-available/xdebug.ini
RUN echo "xdebug.remote_log=/var/log/apache2/xdebug.log" >> /etc/php/7.4/mods-available/xdebug.ini

RUN a2dissite 000-default.conf
RUN a2ensite $URL.conf

RUN a2enmod rewrite
RUN a2enmod ssl

RUN rm -r /var/www/html
RUN mkdir /var/www/$URL
RUN chown -R www-data:www-data /var/www/$URL

COPY php.ini /etc/php/7.4/apache2/
COPY cert/crt /etc/apache2/ssl/
COPY cert/key /etc/apache2/ssl/

RUN phpenmod xdebug
RUN phpenmod tidy

EXPOSE 443

VOLUME /var/www/$URL
VOLUME /var/log/apache2

CMD service apache2 start && tail -f /dev/null