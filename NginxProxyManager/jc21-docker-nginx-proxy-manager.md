
```sh
mkdir docker
```
```sh
mkdir nginx-proxy-manager
```
```sh
cd nginx-proxy-manager
```
```sh
nano docker-compose.yml
```
```sh
services:
  nginx-proxy-manager:
    image: jc21/nginx-proxy-manager
    container_name: nginx-proxy-manager
    ports:
      - 80:80
      - 81:81
      - 443:443
    volumes:
      - /root/docker/volumes/nginx-proxy-manager/data:/data
      - /root/docker/volumes/nginx-proxy-manager/letsencrypt:/etc/letsencrypt
      - restart: unless-stopped



```      

```sh
docker compose up -d
```
