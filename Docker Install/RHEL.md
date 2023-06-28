
```sh
sudo dnf config-manager \
--add-repo=https://download.docker.com/linux/centos/docker-ce.repo
```

```sh
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/rhel/docker-ce.repo
```

```sh
sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

#### Remove Docker 
```sh
sudo yum remove -y docker-ce docker-ce-cli
```



------------------------------------------------------------------------------

```sh
sudo dnf config-manager \
--add-repo=https://download.docker.com/linux/centos/docker-ce.repo

nano /etc/yum.repos.d/docker-ce.repo

[docker-ce-stable]
name=Docker CE Stable - $basearch
baseurl=https://download.docker.com/linux/centos/$releasever/$basearch/stable # <--- Correct URL
enabled=1
gpgcheck=1
gpgkey=https://download.docker.com/linux/centos/gpg


(replace fedora with centos )



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
