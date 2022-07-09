# How to install wordpress using docker-compose 

```sh
version: '3.1'

services:

  wordpress:
    image: wordpress
    restart: unless-stopped
    ports:
      - 8181:80
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: wp-securepassword
      WORDPRESS_DB_NAME: testwpdb
    volumes:
      -/AppData/conf/Wordpress:/var/www/html
    links:
      - db:db

  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_DATABASE: testwpdb
      MYSQL_USER: wpuser
      MYSQL_PASSWORD: wp-securepassword
      MYSQL_RANDOM_ROOT_PASSWORD: '1'
    volumes:
      - db:/var/lib/mysql

volumes:
  wordpress:
  db:
```
