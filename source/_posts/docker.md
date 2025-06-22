---
title: docker
date: 2021-03-01 14:46:11
tags:
---

# Base
docker-compose down      # 停止并删除容器
docker-compose build    # 重新构建镜像
docker-compose up -d    # 创建并启动容器

## 阿里云服务器
拉取镜像慢
获取 镜像加速器地址：https://cr.console.aliyun.com/cn-shanghai/instances/mirrors
mkdir -p /etc/docker
touch daemon.json
vim daemon.json
{
  "registry-mirrors": ["https://xxxxx.mirror.aliyuncs.com"]
}
systemctl daemon-reload
systemctl restart docker

## 服务器
apt update
apt install -y docker.io=27.5.1-0ubuntu3~22.04.2
apt install docker-compose -y
docker-compose -v
docker-compose version 1.29.2, build unknown


## demo
```yaml
# docker-compose.yaml
version: '3'
services:
  web:
    image: nginx:latest
    ports:
     - "8080:80"
    volumes:
     - ./mysite:/usr/share/nginx/html
```
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
docker images
docker rmi {image-id}

## 验证端口映射
docker port container_name_or_id

## 查看容器内python日志
docker logs my-python-app


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

# Java项目 docker 打包
## 项目根目录创建 Dockerfile 文件
```
FROM openjdk:8-jdk-alpine
VOLUME /tmp
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories
RUN apk add --no-cache tzdata bash  ttf-dejavu fontconfig \
	&& fc-cache --force
RUN echo "Asia/Shanghai" > /etc/timezone
ADD target/app.jar app.jar
RUN sh -c 'touch /*.jar'
EXPOSE 8080
ENV apmOpts=""
ENTRYPOINT ["sh", "-c", "java $apmOpts -Djava.security.egd=file:/dev/./urandom -jar /app.jar"]
```

## 构建 Spring Boot 项目
mvn clean
mvn package

## 构建 docker 镜像
docker build -t my-spring-boot-app .

## 运行 docker 容器
docker run -p 8080:8080 my-spring-boot-app

## 使用 docker-compose.yml
```yml
version: '3.8'

services:
  api-dev:
    container_name: spring-api-dev
    build: .
    ports:
      - "8080:8080"
    environment:
      - SPRING_PROFILES_ACTIVE=dev
    restart: always

  api-prod:
    container_name: spring-api-prod
    build: .
    ports:
      - "8080:8080"
    environment:
      - SPRING_PROFILES_ACTIVE=prod
    restart: always
```

### 创建容器
docker-compose build

### 指定环境变量
```zsh
$ docker-compose up --build api-dev
spring-api-dev  | true
spring-api-dev  | https://d.x.cn

$ docker-compose up --build api-prod 
spring-api-prod  | false
spring-api-prod  | https://p.x.cn
```

# docker配置模板

## mysql轻量级
/root/docker/mysql/docker-compose.yml
```yml
version: '3.8' # 指定 docker-compose 文件版本

services:
  mysql-low: # 定义服务名称，可以自定义，这里与容器名保持一致
    image: mysql:5.7 # 指定使用的镜像
    container_name: mysql-low # 指定容器名称，与 docker run --name 对应
    environment: # 设置环境变量，与 docker run -e 对应
      MYSQL_ROOT_PASSWORD: xxxxx
    ports: # 端口映射，与 docker run -p 对应
      - "3306:3306" # 将宿主机的 3306 端口映射到容器的 3306 端口
    volumes: # 卷挂载，与 docker run -v 对应
      # 数据卷挂载 (将宿主机的 /mydata/mysql 映射到容器的 /var/lib/mysql)
      - /mydata/mysql:/var/lib/mysql
      # 配置文件挂载 (将宿主机的 /root/workspace/config/mysql_custom.cnf 映射到容器内的配置目录)
      # 注意：通常将自定义配置挂载到 /etc/mysql/conf.d/ 目录下，MySQL 会自动加载
      - /root/docker/mysql/mysql_custom.cnf:/etc/mysql/conf.d/mysql_custom.cnf
    deploy: # 资源限制，对应 --memory 和 --cpus
      resources:
        limits:
          cpus: "0.5" # 限制 CPU 使用最多为 0.5 核
          memory: "512m" # 限制内存使用最多为 512MB
    restart: always # 可选：添加重启策略，比如容器退出时总是自动重启
```

### 依赖的数据库设置文件
/root/docker/mysql/mysql_custom.cnf
```cnf
[mysqld]
sql_mode = "ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION"
```

# ISSUES
## docker Can't close tar writer: io: read/write on closed pipe
把客户端打开

## 一个前端项目中，在根目录有docker-compose.yml 和 Dockerfile 两个文件，这两个文件分别是什么，做什么，有什么联系
Dockerfile和docker-compose.yml是Docker生态系统中常用的两种文件，它们扮演着不同但相互补充的角色。在前端项目中，这两个文件的存在表明开发者选择使用Docker来容器化应用及其依赖的环境，从而实现一致性、便捷的部署和环境管理。
Dockerfile
Dockerfile是一个文本文件，其中包含了一系列的指令和参数，用于自动构建镜像。每个指令都会在镜像中创建一层，这些指令包括拷贝文件、设置环境变量、安装依赖等。通过Dockerfile指定的这些指令，Docker可以自动构建出一个可用来运行应用的镜像。
对于一个前端项目来说，Dockerfile通常会完成以下操作：
- 设置基础镜像，比如node或nginx，这取决于你如何打算运行或服务你的前端项目。
- 拷贝项目文件到镜像内。
- 安装项目依赖。
- 构建项目（如果是需要编译的前端框架，如React、Vue等）。
- 配置镜像，使其在容器启动时运行项目。

docker-compose.yml
docker-compose.yml是一个用于定义和运行多容器Docker应用的配置文件。通过docker-compose命令，你可以利用此文件配置应用服务的相关属性，比如容器、网络、卷等。它是YAML格式的，可以简化容器部署过程中的命令行参数。
对于前端项目，docker-compose.yml可能会用来：
- 定义前端服务容器，这个容器基于Dockerfile构建的镜像。
- 配置前端应用依赖的其他服务，比如后端API、数据库服务等，实现多服务的联合部署和本地开发。
- 配置网络、挂载卷等，以支持更复杂的开发和部署需求。

它们之间的联系
Dockerfile和docker-compose.yml的联系在于docker-compose.yml可以引用Dockerfile来构建应用镜像。在docker-compose.yml中，你可以指定服务使用基于Dockerfile构建的本地镜像，或者直接使用远程仓库中的镜像。这意味着你可以在docker-compose.yml文件中利用Dockerfile来精确控制应用容器的构建过程、环境和行为。
简而言之，Dockerfile定义了如何构建镜像，而docker-compose.yml定义了如何在一定配置下运行这个镜像（以及可能的其他相关服务）。

Dockerfile
```
FROM registry.cn-shanghai.aliyuncs.com/ethbase/uniapp-node:v1

RUN mkdir -p /home/src/release/ethi/

WORKDIR /home

ADD ./settings.json .
ADD ./dist/ src/release/ethi
```
docker-compose.yml
```yml
version: '3'
services:
  cms:
    build:
      context: .
      dockerfile: Dockerfile
    environment:
      proxyUrl: http://hcp-bg
    ports:
      - "8080:8080"
```