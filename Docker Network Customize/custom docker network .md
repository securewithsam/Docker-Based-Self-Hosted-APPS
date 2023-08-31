
 
###  RHEL - How to change the docker0 container IP range if its conflicting with similar subnet on the network .

### Check the IP Address/subnet of the current network 
```sh
ip add show br-2f18408fb94d
```
### Check current docker network 
```sh
docker network ls
```
### Inspect current network
```sh
docker network inspect br-2f18408fb94d
```

#### Stop the Docker Service
```sh
systemctl stop docker.service
```
#### Check status of the Docker Service
```sh
systemctl status docker.service
```
#### Bring the desired interface down 
```sh
ip link set dev br-2f18408fb94d down
```

#### Specify custom network subnet (RHEL, Centos)
```sh
nano /etc/sysconfig/docker-network 
```
```sh
{
    "bip": "192.168.9.0/16"
}

```

#### Verify old routes 
```sh
iptables -t nat -L -n
```

#### Remove default subnets MASQUARADE rules from the POSTROUTING chain in newtwork iptables
```sh
iptables -t nat -F POSTROUTING
```
#### Flush docker rules 
```sh
iptables -F DOCKER
```

#### Start Docker Service and it will create the docker route automatically 
```sh
systemctl start docker.service
```

#### Check status of the Docker Service
```sh
systemctl status docker.service
```

#### Verify if IP forwarding is enabled 
```sh
sysctl net.ipv4.conf.all.forwarding
```

#### Verify MASQUARADE rule has new subnet address
```sh
iptables -t nat -L -n
```
#### Bring the desired interface up 
```sh
ip link set dev br-2f18408fb94d up
```

#### Validation
```sh
docker network inspect br-2f18408fb94d
```
```sh
ip add show br-2f18408fb94d
```
