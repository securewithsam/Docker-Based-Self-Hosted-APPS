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
                  runc
```
```sh
sudo dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo

```
```sh
sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
```sh
sudo systemctl start docker
```




----------------------------------------------------------------------------------------------


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
