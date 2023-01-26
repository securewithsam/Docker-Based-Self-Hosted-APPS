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

```sh
'trusted_domains' =>
  array (
   0 => 'localhost',
   1 => 'server1.example.com',
   2 => '192.168.1.50',
   3 => '[fe80::1:50]',
),
```

#### Increase File Size Uploads with .htaccess

```sh
php_value memory_limit 2G
php_value upload_max_filesize 16G
php_value post_max_size 16G
php_value max_input_time 3600
php_value max_execution_time 3600
```

### copy paste the above on the location below and save and restart next cloud container app

```sh
nano /var/www/html/.htaccess
```
