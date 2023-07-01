### Issue : No network after installing docker ,due to docker network confilict 
#### Change docker0 network subnet .Use any network that doesn't conflict your internal networks.

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

#### Stop the Docker Service
```sh
systemctl stop docker.service
```
#### Bring down the Docker bridge docker0
```sh
ip link set dev docker0 down
```
####Verify if IP forwarding is enabled 
```sh
sysctl net.ipv4.conf.all.forwarding
```

#### Specify custom network subnet (RHEL, Centos)
```sh
nano /etc/sysconfig/docker-network 
```
```sh
DOCKER_NETWORK_OPTIONS="--bip=192.3.3.3/24"
```
#### Remove default subnets MASQUARADE rules from the POSTROUTING chain in newtwork iptables
```sh
iptables -t nat -F POSTROUTING
iptables -F DOCKER
```
#### Start Docker Service
```sh
systenctl start docker.service
```
#### VerifyMASQUARADE rule has new subnet address
```sh
iptables -t nat -L -n
```

#### Validation
```sh
docker network inspect bridge
```
