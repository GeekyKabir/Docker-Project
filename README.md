# Docker-Project
Docker Training Project Under IIEC RISE 1.0 
Creating and configuring  Web Server using Mariadb:latest and Wordpress:5.1.1php7.33-apache using Docker in RedHat8.
In this project I am hosting a website with my own created server by using the docker container.
Below is the code given which have to be present in the file docker-compose.yml 
Here, we are using Docker images: Wordpress:5.1.1php7.3-apache and Mariadb:latest version and Docker-compose, for client side I am using mysql and to expose this website to outside world, we are using bridge adapter and in this I am using the concept NATing.
#docker-compose.yml
version: '3'

services:
  dbos:
    image: mariadb
    volumes:
      - datastorage:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: rhrootpass
      MYSQL_USER: kabir
      MYSQL_PASSWORD: kabir@redhat
      MYSQL_DATABASE: mydb

  wpos:
    image: wordpress:5.1.1-php7.3-apache
    restart: always
    depends_on:
      - dbos
    ports:
      - 8081:80
    environment:
      WORDPRESS_DB_HOST: dbos
      WORDPRESS_DB_USER: kabir
      WORDPRESS_DB_PASSWORD: kabir@redhat
      WORDPRESS_DB_NAME: mydb
    volumes:
      - webstorage:/var/www/html

volumes:
  datastorage:
  webstorage:
