## Guacamole 

version: "3.1"
 
services:
 
# Configure MariaDB with persistent storage
  database:
    image: mariadb:10.0
    hostname: db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD_FILE: '/run/secrets/mysql-root'
      MYSQL_DATABASE: 'guacamole_db'
      MYSQL_USER: 'guacamole_user'
      MYSQL_PASSWORD: '/run/secrets/guacamole-user'
    container_name: db 
    volumes:
      - "db:/var/lib/mysql"
    secrets:
      - mysql-root
      - guacamole-user
 
# Configure proxy daemon
  guacd:
    image: guacamole/guacd:1.5.2
    container_name: guacd
    restart: always
 
# Configure and link Guacamole to db and proxy
# expose port 8080 to host.
  guacamole:
    image: guacamole/guacamole:1.5.2
    container_name: guacamole
    restart: always
    ports:
      - 8080:8080
    links:
      - guacd
      - database
    environment:
      GUACD_HOSTNAME: guacd
      MYSQL_HOSTNAME: db
      MYSQL_DATABASE: guacamole_db
      MYSQL_USER: guacamole_user
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
    secrets:
      - guacamole-user
 
secrets:
  mysql-root:
    file: mysql-root
  guacamole-user:
    file: guacamole-user
 
# This volume has to be created before docker-compose up
volumes:
  db:
    external: true
