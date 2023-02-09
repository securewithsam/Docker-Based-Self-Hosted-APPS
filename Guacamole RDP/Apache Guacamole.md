#Guacamole RDP
Need Docker-CE and Docker-Compose
mkdir docker
mkdir guacamole
cd guacamole
nano docker-compose.yml

```sh
version: "3"
services:
  guacamole:
    image: jwetzell/guacamole
    restart: always
    container_name: guacamole
    volumes:
      - ./postgres:/config
    ports:
      - 8280:8080
    environment:
      - EXTENSIONS=auth-totp
volumes:
  postgres:
    driver: local
```    
    
save the file with CTRL + O, then press Enter to confirm, and exit the nano text editor with CTRL + X

```sh
docker-compose up -d
```
docker-compose logs -f
http://xx.xx.xx.xx:8280

username: guacadmin
password: guacadmin



*** permission Denied Error while pulling up docker compose -run commands below***

```sh
sudo chmod +x /usr/local/bin/docker-compose;
sudo usermod -aG docker $USER
sudo chgrp docker /usr/local/bin/docker-compose
sudo chmod 750 /usr/local/bin/docker-compose  
```




------------------------

Install docker compose

```sh
curl -sL "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```
```sh
docker-compose --version
```
