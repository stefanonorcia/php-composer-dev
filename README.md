# php-composer-dev

This is the docker compose I use when developing PHP projects: Ubuntu 20.04 Apache2, PHP 7.4, XDebug, MariaDB.

## Requirements

1. Install [Docker](http://docker.io).
2. Install [Docker-compose](http://docs.docker.com/compose/install/).
3. Clone this repository

## Configure the build

All the parameters can be set in the `.env` file in the root of the project. You can set the URL and MariaDB environment variables in this file then the compose will build the containers accordingly.

```
URL=www.example.com
MYSQL_ROOT_PASSWORD=example
MYSQL_USER=example
MYSQL_DATABASE=example
MYSQL_PASSWORD=example
```
Remember to add the SSL certificates for your domain in the ./contextHttpd/certs, you can follow THIS guide to create a certification authority and self sign your own certificates.

```
random@checkmate:~/Documents/blog/lamp_docker/contextHttpd/cert$ ll
total 16
drwxr-xr-x  4 random  staff   128 Aug 26 22:00 ./
drwxr-xr-x  6 random  staff   192 Aug 27 17:42 ../
-rw-r--r--  1 random  staff  1610 Oct 18  2019 crt
-rw-r--r--  1 random  staff  1675 Oct 18  2019 key
```

##Usage

```
docker-compose up -d httpd mariadb
```





