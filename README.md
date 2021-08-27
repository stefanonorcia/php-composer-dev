# php-composer-dev
This is the docker compose I use when developing PHP projects: Ubuntu 20.04 Apache2, PHP 7.4, XDebug, MariaDB.

The Docker Compose is parametric, you can change the URL argument to match the domain you want to use, the Apache2 Dockerfile will build the Apache configuration and create the directory in /var/www based on the URL parameter.

The URL parameter can be set in the .env file in the root of the console and the composer.

The URL parameter is also used in the Compose file to automatically mount the website directory in the Apache2 container to the ./www directory, you also have Apache2 log directory automatically mounted in the ./logs/apache2 directory.

You can configure the MariaDB server in ./contextMariadb/mariadb.env file.

Remember to add the SSL certificates for your domain in the contextHttpd/certs, you can follow THIS guide to create a certification authority and self sign your own certificates.

Remember also to add the URL domain to your host file.