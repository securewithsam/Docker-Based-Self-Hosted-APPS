####  Status code: 404 for https://download.docker.com/linux/rhel/8/x86_64/stable/repodata/repomd.xml (IP: 13.224.20.74)

```sh
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine \
                  podman \
                  runc -y
```
```sh
sudo dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo -y

```
```sh
sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```
```sh
nano /etc/docker/daemon.json
```
```sh
{
	"live-restore": true,
	"bip": "10.10.3.1/24",
	"default-address-pools": [{
		"base": "10.0.3.0/24",
		"size": 24
	}]
}
```
```sh
sudo systemctl restart docker
```

----------------------------------------------------------------------------------------------
#### Optional

```sh
sudo dnf config-manager \
--add-repo=https://download.docker.com/linux/centos/docker-ce.repo
```
```sh
nano /etc/yum.repos.d/docker-ce.repo
```
```sh
[docker-ce-stable]
name=Docker CE Stable - $basearch
baseurl=https://download.docker.com/linux/centos/$releasever/$basearch/stable # <--- Correct URL
enabled=1
gpgcheck=1
gpgkey=https://download.docker.com/linux/centos/gpg
```

(replace fedora with centos )


```sh
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine \
                  podman \
                  runc


```
