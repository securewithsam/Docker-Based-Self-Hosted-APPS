Install Portainer

```sh
docker volume create portainer_data
```
```sh
docker run -d -p 9000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

## Or
```sh
sudo docker run -d \
--name="portainer" \
--restart on-failure \
-p 9000:9000 \
-v /var/run/docker.sock:/var/run/docker.sock \
-v portainer_data:/data \
portainer/portainer-ce             

```
