#### How to setup OMADA Controller using Docker .

```sh
docker volume create omada-data
docker volume create omada-work
docker volume create omada-logs
```
```sh
docker run -d \
    --name omada-controller \
    --restart unless-stopped \
    --net host \
    -e MANAGE_HTTP_PORT=8088 \
    -e MANAGE_HTTPS_PORT=8043 \
    -e PORTAL_HTTP_PORT=8088 \
    -e PORTAL_HTTPS_PORT=8843 \
    -e SHOW_SERVER_LOGS=true \
    -e SHOW_MONGODB_LOGS=false \
    -e SSL_CERT_NAME="tls.crt" \
    -e SSL_KEY_NAME="tls.key" \
    -e TZ=Etc/UTC \
    -v omada-data:/opt/tplink/EAPController/data \
    -v omada-work:/opt/tplink/EAPController/work \
    -v omada-logs:/opt/tplink/EAPController/logs \
    mbentley/omada-controller:latest
```

#### Docker-Compose

```sh
name: omada controller
services:
    omada-controller:
        container_name: omada-controller
        restart: unless-stopped
        network_mode: host
        environment:
            - MANAGE_HTTP_PORT=8088
            - MANAGE_HTTPS_PORT=8043
            - PORTAL_HTTP_PORT=8088
            - PORTAL_HTTPS_PORT=8843
            - SHOW_SERVER_LOGS=true
            - SHOW_MONGODB_LOGS=false
            - SSL_CERT_NAME=tls.crt
            - SSL_KEY_NAME=tls.key
            - TZ=Etc/UTC
        volumes:
            - omada-data:/opt/tplink/EAPController/data
            - omada-work:/opt/tplink/EAPController/work
            - omada-logs:/opt/tplink/EAPController/logs
        image: mbentley/omada-controller:latest
volumes:
    omada-data:
        external: true
        name: omada-data
    omada-work:
        external: true
        name: omada-work
    omada-logs:
        external: true
        name: omada-logs


```
