# Install, Setup & Configure Wireguard

```sh
sudo apt-get update && sudo apt-get upgrade -y
```
```sh
curl -fsSL https://get.docker.com -o get-docker.sh
```
```sh
sh get-docker.sh
```
```sh
sudo curl -L --fail https://raw.githubusercontent.com/linuxserver/docker-docker-compose/v2/run.sh -o /usr/local/bin/docker-compose
```
```sh
sudo chmod +x /usr/local/bin/docker-compose
```
```sh
sudo mkdir /opt/wireguard-server
```
```sh
sudo chown ubuntu:ubuntu /opt/wireguard-server
```
```sh
nano /opt/wireguard-server/docker-compose.yaml
```
Paste below 
```sh
version: "2.1"
services:
  wireguard:
    image: linuxserver/wireguard
    container_name: wireguard
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/Toronto
      - SERVERPORT=51820 #optional
      - PEERS=100 #optional
      - PEERDNS=auto #optional
      - INTERNAL_SUBNET=10.13.13.0 #optional
    volumes:
      - /opt/wireguard-server/config:/config
      - /lib/modules:/lib/modules
    ports:
      - 51820:51820/udp
    sysctls:
      - net.ipv4.conf.all.src_valid_mark=1
    restart: unless-stopped
```
```sh
cd /opt/wireguard-server/
```
```sh
docker-compose up -d
```
to view qr code to connect on mobile
```sh
sudo docker exec -it wireguard /app/show-peer 1 
```
to copy connection info to connect in windows/mac
```sh
cat /opt/wireguard-server/config/peer1/peer1.conf   
```

                                                       ****IMPORTANT****

# MAKE SURE TO OPEN PORT 51820 ON THE CLOUD INSTANCE 




## If you want to share the connection then use below command to get different peer info to connect in windows/mac

```sh
cat /opt/wireguard-server/config/peer2/peer2.conf
```
```sh
cat /opt/wireguard-server/config/peer3/peer3.conf
```
```sh
cat /opt/wireguard-server/config/peer4/peer4.conf
```


## If you want to share the connection then use below command to get different peer info to connect on mobile devices via QR code
```sh
sudo docker exec -it wireguard /app/show-peer 10
```
```sh
sudo docker exec -it wireguard /app/show-peer 11
```
```sh
sudo docker exec -it wireguard /app/show-peer 12
```
```sh
docker-compose up -d --force-recreate
```
