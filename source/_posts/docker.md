---
title: docker
date: 2021-03-01 14:46:11
tags:
---

# Base
## CLI
启动容器：docker start container_name 
关闭容器：docker stop container_name
查看运行容器：docker ps
容器列表：docker ps -a

### 创建镜像
docker-compose build
docker images
停止然后删除容器和网络
docker-compose down
docker-compose up

## 创建容器
```
$ sudo docker run --name nginxvuemd -v /Users/niekaifa/test/vuem_data.conf:/etc/nginx/conf.d/default.conf -v /Users/niekaifa/ikyu/KilFront/vue-project/dist:/data -d -p 8072:8072 nginx
```

## 删除容器
docker rm 容器的名称或者 ID

## 停止容器
docker stop 容器的名称或者 ID

## 删除镜像
docker rmi {image-id}


## 获取容器/镜像
```
$ docker pull mongo
```
### 查看镜像信息
```
$ docker images mongo
REPOSITORY    TAG      IMAGE ID      CREATED        VIRTUAL SIZE
mongo         latest   50fa1fa47718  11 hours ago   402 MB
```
### 元数据
docker inspect nginx

## 启动容器
该镜像中默认会在27017端口启动 MongoDB，当然这里需要开启端口映射，使 MongoDB 容器对外网访问开放。
```
$ docker run --name mongo -v /home/docker/mongo:/data/db -p 27017:27017 -d mongo
```
参数说明：
* -v：创建一个位置 /home/docker/mongo数据卷并挂载到容器的/data/db位置
* -p：指定容器27017端口映射到本地宿主27017端口，以便mongo裸露在外网 
* -d：守护态运行mongo

### 成功启动
```
$ docker ps -a
CONTAINER ID   IMAGE   COMMAND          CREATED         STATUS        PORTS                      NAMES
d83cab80f13d   mongo   "/entrypoint.sh  3 seconds ago   Up 2 seconds   0.0.0.0:27017->27017/tcp   mongo
```

## 创建并启动项目
``` bash
./build.sh
chmod 777 build.sh
docker-componse up
```

## 官方镜像
https://hub.docker.com/search?image_filter=official&q=

# ISSUES
## docker Can't close tar writer: io: read/write on closed pipe
把客户端打开