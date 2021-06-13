# Description of the project

1. The config file is created using docker-compose to initialize and run Wordpress.
2. After initialization, install the two-factor plugin for Wordpress and activate it.

**docker-compose.yml**

```
version: '3.3'
services:
  db:
    container_name: 'local-wordpress-db'
    image: 'mariadb:10.4'
    volumes:
      - './data/mysql:/var/lib/mysql'
    ports:
      - 18766:3306
    environment:
      MYSQL_ROOT_PASSWORD: somewordpress
      MYSQL_DATABASE: wordpress_db
      MYSQL_USER: wordpress_user
      MYSQL_PASSWORD: wordpress_password

  wordpress:
    container_name: 'local-wordpress'
    depends_on:
      - db
    image: 'wordpress:latest'
    ports:
      - '80:80'
    environment:
      WORDPRESS_DB_HOST: 'db:3306'
      WORDPRESS_DB_USER: wordpress_user
      WORDPRESS_DB_PASSWORD: wordpress_password
      WORDPRESS_DB_NAME: wordpress_db
    volumes:
      - "./wordpress:/var/www/html"
      - "./plugins:/var/www/html/wp-content/plugins"
```
a plugins folder is created next to the **docker-compose.yml** file, where you need to place a plugin with **two-factor**





# Deployment instructions
## Initial installation requirements
Install **Docker.io** and **Docker Compose:** 
`sudo apt install docker.io docker-compose`
## Create a working directory and change to it
`mkdir docker-project && cd docker-project`
## Clone this project to your directory
`git clone https://github.com/Stovart397/Docker-compose-WordPress-two-factory-plugin.git`
 
 go to directory Docker-compose-WordPress-two-factory-plugin
 
 ## Start the containers:
 `docker-compose up -d`

Go to http://localhost/ and you’ll see WordPress installation screen.

If done correctly, after the initial WordPress installation, Two Factor Authentication should appear on the Dashboard under the plugins section.
# Delete docker image
`docker-compose down`
 
`docker image rm [OPTIONS] IMAGE [IMAGE...]`
