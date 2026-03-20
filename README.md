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

## adding user(current loggin) to group of docker(commands of docker executable only for root and docker(user) by default)
## authorize will be effective in a new shell.
sudo usermod -aG docker $USER

## Dockerfile: container autorun
## 1. make new folder for docker reffers and workspace on host
mkdir -p ~/docker/workspace
mkdir -p ~/hostworkspace
## 2. enter docker workspace, and write Dockerfile
nano Dockerfile
## 2.1. the content of Dockerfile
# 1. 使用 Ubuntu 24.04 作为基础镜像
FROM ubuntu:24.04

# 2. 设置环境变量，防止安装过程中的交互提示
ENV DEBIAN_FRONTEND=noninteractive

# 3. 设置默认工作目录为 /root (即容器内的 ~/)
WORKDIR /root

# 4. 安装基础工具及依赖
RUN apt-get update && apt-get install -y \
    curl \
    git \
    python3 \
    python3-pip \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# 5. 安装 Node.js 24
RUN curl -fsSL https://deb.nodesource.com | bash - \
    && apt-get install -y nodejs

# 6. 声明需要暴露的端口（仅作说明，实际绑定在 run 命令中完成）
EXPOSE 8080 5000 18443

# 7. 默认启动命令
CMD ["/bin/bash"]

## 2.3. build by Dockerfile (cd to the path where Dockerfile located)
docker build -t {{@dockername}}
## 2.4. run docker with mounted and port binding.
## 'name_container': name of the container; 'name_image': name of the image.
docker run -it \
  --name name_container \
  -v ~/myproj:/root/myproj \
  -p 18789:18789 \
  -p 18443:443 \
  -p 8080:80 \
  -p 5000:5000 \
  name_image

## 3. exit container without stop: press Ctrl + P and then Ctrl + Q
## 4. re-enter container
docker exec -it name_container /bing/bash
##5. stop/start container
docker stop name_container
docker start name_container

