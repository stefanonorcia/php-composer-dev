FROM mariadb:10.5-focal

# MARIADB
#docker run
#-p 3306:3306
#-v /Users/random/omicron/httpd/mariadb:/var/lib/mysql
#-v /Users/random/omicron/httpd/logs/mysql:/var/log/mysql
#--name database
#-h database
#--add-host httpd:192.168.0.10
#--net ppp
#--ip 192.168.0.20
#--dns 8.8.8.8
#--dns 4.4.4.4
#mariadb

ENV MYSQL_ROOT_PASSWORD=root
ENV MYSQL_DATABASE=ppp
ENV MYSQL_USER=ppp
ENV MYSQL_PASSWORD=ppp

COPY conf/50-server.cnf /etc/mysql/mariadb.conf.d/

VOLUME /var/log/mysql