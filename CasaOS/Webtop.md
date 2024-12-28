#### Remote Browser Isolation -KASM - Ephemeral Desktop

```sh
---
version: "2"
services:
  webtop:
    #image: linuxserver/webtop:latest
    image: lscr.io/linuxserver/webtop:ubuntu-kde
    container_name: webtop
    restart: unless-stopped
    environment:
      - TZ=America/Toronto # Your local timezone
      - PUID=1000 # Application user ID
      - PGID=1000 # Application group ID
    volumes:
      - /home/infra-admin/docker/webtop/var/run/docker.sock:/var/run/docker.sock # Docker Socket on the system, if you want to use Docker in the container
      - /home/infra-admin/docker/webtopconfig:/config # Application home directory
    ports:
      - 3005:3000/tcp # Web Desktop GUI
```
