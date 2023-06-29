### Issue : No network after installing docker ,due to docker network confilict 
### Change docker0 network subnet .Use any network that doesn't conflict your internal networks.

### Open daemon.json , if its not found , create one.

```sh
 nano /etc/docker/daemon.json
```

```sh
{
  "bip": "192.0.0.1/16"
}

```


Docker Network Troubleshooting 

```sh
route -n
docker network list
```

#### Inspect Docker Network 
```sh
docker network inspect 2f18408fb94d
```

#### Remove Docker Network 
```sh
docker network rm 2f18408fb94d
```

### Add new Docker Network 

```sh
docker network create --driver=bridge --subnet=192.2.0.0/16 br0
```


#### Docker Network Files Path

```sh
cd /var/lib/docker/
```
