#### Method 2 on how to change docker subnet if its clashing 

```sh
sudo nano /etc/docker/daemon.json
```

```sh
{
"log-driver": "journald",
"log-opts": {
"tag": "{{.Name}}"
},
"bip": "172.26.0.1/16"
}
```
```sh
sudo systemctl restart docker
```
```sh
netstat -rn
```
