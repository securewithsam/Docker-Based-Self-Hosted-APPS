#### Installing Docker
https://i12bretro.github.io/tutorials/0696.html

#### install prerequisites
```sh
sudo apt install apt-transport-https ca-certificates curl software-properties-common gnupg-agent -y
```
#### add docker gpg key
```sh
curl -fsSL https://download.docker.com/linux/$(awk -F'=' '/^ID=/{ print $NF }' /etc/os-release)/gpg | sudo apt-key add -
```
#### add docker software repository
```sh
sudo add-apt-repository "deb [arch=$(dpkg --print-architecture)] https://download.docker.com/linux/$(awk -F'=' '/^ID=/{ print $NF }' /etc/os-release) $(lsb_release -cs) stable"
```
#### install docker
```sh
sudo apt install docker-ce docker-compose containerd.io -y
```
#### enable and start docker service
```sh
sudo systemctl enable docker && sudo systemctl start docker
```
#### add the current user to the docker group
```sh
sudo usermod -aG docker $USER
```
#### reauthenticate for the new group membership to take effect
```sh
su - $USER
```

#### Apache Guacamole

#### create working directories
```sh
mkdir ~/docker/mariadb -p
```
#### set owner of docker directory
```sh
sudo chown "$USER":"$USER" ~/docker -R
```
#### download the guacamole container
```sh
docker pull guacamole/guacamole
```
#### run the mariadb docker container
```sh
docker run -d --name mariadb -e MYSQL_ROOT_PASSWORD=r00tp@ss -v ~/docker/mariadb:/var/lib/mysql --restart=unless-stopped mariadb:latest
```
#### create database init script
```sh
docker run --rm guacamole/guacamole /opt/guacamole/bin/initdb.sh --mysql > ~/docker/mariadb/guacamole_db.sql
```
#### connect to mariadb container shell
```sh
docker exec -ti mariadb /bin/bash
```
#### connect to mariadb as root user
```sh
mysql -uroot -pr00tp@ss
```
#### create the database
```sh
create database guacamole;
```
#### create and configure the database user
```sh
GRANT ALL ON guacamole.* TO 'guacamole_rw'@'%' IDENTIFIED BY 'Guac@m0le!';
```
#### flush mariadb privileges
```sh
flush privileges;
```
#### exit mariadb cli
```sh
quit
```
#### import the guacamole schema
```sh
cat /var/lib/mysql/guacamole_db.sql | mysql -uroot -pr00tp@ss -Dguacamole
```
#### exit the maridb container shell
```sh
exit
```
#### run the guacd container
```sh
docker run -d --name guacd guacamole/guacd
```
#### run the guacamole container
```sh
docker run -d --name guacamole --link guacd --link mariadb -e MYSQL_HOSTNAME=mariadb -e MYSQL_DATABASE=guacamole -e MYSQL_USER=guacamole_rw -e MYSQL_PASSWORD=Guac@m0le! -p 8080:8080 guacamole/guacamole
```




 ##### http://DNS-or-IP:8080/guacamole/
 ##### Log in with guacadmin/guacadmin
