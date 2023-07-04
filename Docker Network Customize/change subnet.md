```sh
ip add show br-2f18408fb94d

docker network ls

docker network inspect br-2f18408fb94d

systemctl stop docker.service

systemctl status docker.service

ip link set dev br-2f18408fb94d down

nano /etc/sysconfig/docker-network 

DOCKER_NETWORK_OPTIONS="--bip=192.3.3.3/24"

iptables -t nat -L -n

systemctl start docker.service

systemctl status docker.service

ip add show br-2f18408fb94d

ip link set dev br-2f18408fb94d up
```
