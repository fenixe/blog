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

## 创建表
```sql
create table a (
  id bigint auto_increment primary key,
  no varchar(50) default '' not null unique comment 'no',
  word varchar(300) default '' not null comment 'word'
) comment 'b';
```

## 索引的类型
MySQL 支持的索引方法主要有以下几种：
BTREE：B 树索引，适用于全键值、键值范围或键值排序的查询，能够加快数据访问速度。它保持数据的排序，并允许搜索、顺序访问、插入和删除等操作在对数复杂度内完成。这是最常见的索引类型。
HASH：哈希索引，基于哈希表实现，适用于等值查询，即完全匹配索引所有列的查询。因为它只有精确匹配索引键的查询才有效，所以它对于范围查询不是很有效。这种类型的索引在 MEMORY（HEAP）存储引擎中使用较多。
FULLTEXT：全文索引，适合对文本内容执行全文搜索。它不是基于单个列的值在字典中的排列顺序，而是通过匹配文本内的关键词来提高搜索效率。只有在 MyISAM 和 InnoDB 存储引擎的表中能够创建全文索引。
RTREE：R 树索引，主要用于空间数据类型，如 MySQL 中的 GEOMETRY 类型，可以实现多维空间数据的索引。这种索引方法一般用在 GIS（地理信息系统）数据中。

# ClickHouse
## 安装
curl -O 'https://builds.clickhouse.com/master/macos/clickhouse' && chmod a+x ./clickhouse
./clickhouse client -h 192.168.2.143 --port 8123 -u default --password ethicall --database rpa