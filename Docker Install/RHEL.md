
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
