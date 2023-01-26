### Portainer Stack

```sh
version: '2'

services:
  db:
    image: mariadb:10.5
    restart: always
    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW
    volumes:
      - /volume1/docker/Nextcloud/database:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=r3#fs)g+ukJ~H>$U
      - MYSQL_PASSWORD=r3#fs)g+ukJ~H>$U
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud

  app:
    image: nextcloud
    restart: always
    ports:
      - 8052:443
    links:
      - db
    volumes:
      - /volume1/docker/Nextcloud/config:/var/www/html
    environment:
      - MYSQL_PASSWORD=r3#fs)g+ukJ~H>$U
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_HOST=db
   
```   


#### For Access through untrusted domain Error

###Login to the CLI of Docker
```sh
apt install nano 
```
```sh
nano /var/www/html/config/config.php
```
