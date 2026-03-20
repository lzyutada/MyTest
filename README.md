# MyTest
For tests of projects

----------------------------------------------------------
## Ubuntu
### installing features
refers to [Ubuntu 24.04 安装 Docker](https://cloud.tencent.com/developer/article/2583690)
- should know: 
```
## take a look at the server that what installings(and the latest ver) avaliable on server.
sudo apt update

## update(installing) from server
sudo apt upgrade

## or both. '&&' continue when the prev is success; -y yes automaticlly
sudo apt update && sudo apt upgrade -y
```

- installing docker
```
## installing index and dependencies
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common

## make a folder for GPG storage
sudo install -m 0755 -d /etc/apt/keyrings

## downloading GPG key
sudo curl -fsSL http://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc

## set power for user to read key file
sudo chmod a+r /etc/apt/keyrings/docker.asc

## set resource source for installation
sudo echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] http://mirrors.aliyun.com/docker-ce/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

## update source list when new source (for docker) added.
sudo apt update

## installing docker
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

## take a look at the version of docker (installing succeed)
docker -v

```
Extra
```
## make docker service run automaticly when sys start.
systemctl is-enabled docker

## setting sources for docker images(the official provided images)
## writing these to /etc/docker/daemon.js
##{
##  "registry-mirrors": [
##    "https://docker.m.daocloud.io",
##    "http://hub-mirror.c.163.com",
##    "https://docker.nju.edu.cn"
##  ]
##}

## restart docker
sudo systemctl restart docker

## run a final test
sudo docker container run hello-world
```
