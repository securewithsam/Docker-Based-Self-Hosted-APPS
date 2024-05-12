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

### Visit the Omda webUI with https://IP:8043

#### Docker-Compose

```sh
version: "3.1"

services:
  omada-controller:
    container_name: omada-controller
    image: mbentley/omada-controller:5.13
    restart: unless-stopped
    ulimits:
      nofile:
        soft: 4096
        hard: 8192
    stop_grace_period: 60s
    network_mode: host
    environment:
      - PUID=1000
      - PGID=1000
      - MANAGE_HTTP_PORT=8088
      - MANAGE_HTTPS_PORT=8043
      - PORTAL_HTTP_PORT=8088
      - PORTAL_HTTPS_PORT=8843
      - PORT_APP_DISCOVERY=27001
      - PORT_ADOPT_V1=29812
      - PORT_UPGRADE_V1=29813
      - PORT_MANAGER_V1=29811
      - PORT_MANAGER_V2=29814
      - PORT_DISCOVERY=29810
      - PORT_TRANSFER_V2=29815
      - PORT_RTTY=29816
      - SHOW_SERVER_LOGS=true
      - SHOW_MONGODB_LOGS=false
      - SSL_CERT_NAME=tls.crt
      - SSL_KEY_NAME=tls.key
      - TZ=Etc/UTC
    volumes:
      - omada-data:/opt/tplink/EAPController/data
      - omada-logs:/opt/tplink/EAPController/logs

volumes:
  omada-data:
  omada-logs:

```
