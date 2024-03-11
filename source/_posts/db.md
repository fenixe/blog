---
title: db
date: 2024-01-31 16:50:54
categories:
- db
tags:
- db
---

# Mongo
## docker
docker run -d -p 27017:27017 --name mongodb mongo:latest


# Mysql
## docker
docker run --name mysql -e MYSQL_ROOT_PASSWORD=123456 -p 3306:3306 -d mysql:latest

docker run -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql

## 删除
系统偏好设置面板中可以看到之前安装的MySQL，此时若想卸载MySQL

ps -ef|grep mysql
彻底删除mysql，停止服务
sudo kill -TERM 1526
相关文件
   sudo rm -rf /usr/local/opt/mysql@5.7
   sudo rm -rf /usr/local/var/mysql
系统配置文件
   sudo rm -rf ~/Library/Preferences/com.mysql.*
   sudo rm -rf ~/Library/LaunchAgents/com.mysql.*
shell 配置文件（.bash_profile, .bashrc 或 .zshrc 等），并删除任何指向MySQL的路径或别名。

## MacOS中查看
mysql -V

# ClickHouse
## 安装
curl -O 'https://builds.clickhouse.com/master/macos/clickhouse' && chmod a+x ./clickhouse
./clickhouse client -h 192.168.2.143 --port 8123 -u default --password ethicall --database rpa