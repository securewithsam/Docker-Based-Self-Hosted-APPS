How to change the network used by Docker?
By default, Docker virtualization system uses 172.17.0.0/12 networks for its operation. If your equipment uses addresses from these networks, you can change the Docker settings. This will prevent possible network conflicts.


#### Request the list of networks:
```sh
docker network list
```
```sh
#### An example of response

NETWORK ID          NAME                          DRIVER              SCOPE
14a38927e118        bridge                        bridge              local
b91a38ed491b        dci_auth                      bridge              local
7bdf76184b18        docker_ipmi_proxy_v2_bridge   bridge              local
2d9237551d88        etc_default                   bridge              local
f67c6099ef24        host                          host                local
cbb6fb4096c5        none                          null                local
```

#### Request the information about the address space used:

An example of commands with responses
```sh
[root@dci ~]# docker network inspect etc_default | grep Subnet
"Subnet": "172.19.0.0/16",
[root@dci ~]# docker network inspect docker_ipmi_proxy_v2_bridge | grep Subnet
"Subnet": "172.26.0.0/16",
[root@dci ~]# docker network inspect bridge | grep Subnet
"Subnet": "172.17.0.0/16",
[root@dci ~]# docker network inspect dci_auth | grep Subnet
"Subnet": "172.25.0.0/16",
```

#### Changing the network for DockerLink to Changing the network for Docker
To change the settings of networks used by Docker:
```sh
Edit or create the nano/etc/docker/daemon.json file:

An example of file
```sh
{
	"live-restore": true,
	"bip": "10.10.0.1/16",
	"default-address-pools": [{
		"base": "10.0.0.0/8",
		"size": 16
	}]
}
```sh

 Comments to the file format
#### Delete all running docker containers:
```sh
docker rm -f `docker ps -q -a`
```

#### Delete all unused Docker objects:
```sh
docker system prune
docker network prune
```

#### Restart the Docker service: 
```sh
systemctl restart docker
```
#### Run DCImanager 6:
```sh
dci start
```

#### Run the BMC proxy module's docker containers:
```sh
docker-compose -f /opt/ispsystem/ipmi_proxy_service/etc/docker/ipmi_proxy_v2.yml up -d
```

#### Run docker containers for working with locations:
```sh
docker-compose -f /opt/ispsystem/dci/etc/location.yaml up -d
```

#### Reboot the server with DCImanager 6:
```sh
reboot
```
#### Check the network settings:
```sh
Examples of commands with responses

[root@dci6 ~]# docker network inspect bridge | grep Subnet
"Subnet": "10.10.0.0/16",
[root@dci6 ~]# docker network inspect dci_auth | grep Subnet
"Subnet": "10.0.0.0/16",
[root@dci6 ~]# docker network inspect docker_ipmi_proxy_v2_bridge | grep Subnet
"Subnet": "10.1.0.0/16",
[root@dci6 ~]# docker network inspect etc_default | grep Subnet
"Subnet": "10.2.0.0/16",
```

