### Remove Installed Binaries for Docker Compose 

```sh
sudo rm -r /usr/bin/docker-compose
sudo rm -r /usr/local/bin/docker-compose
```

### Install Docker-Compose

```sh
cd ~/

sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

docker-compose --version
```
