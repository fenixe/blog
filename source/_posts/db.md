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

### 索引KEY
```sql
CREATE TABLE `reocrd` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `no` varchar(20) NOT NULL DEFAULT '' COMMENT '号',
  PRIMARY KEY (`id`),
  KEY `idx_reocrd_no` (`no`)
) ENGINE=InnoDB AUTO_INCREMENT=4431 DEFAULT CHARSET=utf8mb4 COMMENT='记录';
```
在MySQL中，KEY关键字通常用于指定索引。在您提供的表结构中，KEY后面跟着的idx_reocrd_no是一个索引的名称，而(no)指示这个索引是基于no这个列建立的。这意味着no列会被用来创建一个索引，以提升根据no列进行查询的性能。
这里是对给出的表结构的详细解释：
- id列被设置为表的主键（PRIMARY KEY），这是一个bigint(20)类型的字段，它是不允许为空的（NOT NULL），会自动递增（AUTO_INCREMENT）。主键是表的唯一标识，对于每个表，主键的值必须是唯一的。
- no列是一个varchar(20)类型的字段，也是不允许为空的（NOT NULL），默认值是空字符串（DEFAULT ''）。COMMENT后面跟的字符串描述了这个列的用途。
- PRIMARY KEY (id)指定了表的主键，这里是id列。
- KEY idx_reocrd_no (no)定义了一个非主键索引（也称为次级索引）。索引的名字是idx_reocrd_no，索引基于no列。这个索引不是表的唯一标识，可以有重复值。创建这样一个索引，主要是为了加快基于no列的查询操作，尤其是当no列在查询条件中经常被使用时。
- ENGINE=InnoDB指定了表使用的存储引擎，InnoDB是MySQL的默认存储引擎，支持事务处理、行级锁定和外键。
- AUTO_INCREMENT=4431指定了id列的自动递增计数将从4431开始。
- DEFAULT CHARSET=utf8mb4指定了表的默认字符集是utf8mb4，这是一个支持存储unicode字符的字符集，它可以存储任何可能出现的字符（包括Emoji表情）。
- COMMENT='记录'在创建表的最后，提供了这个表的注释信息，这里表示表的用途或描述是“记录”。
所以，在您的表中，存在两个索引：主键索引（基于id字段）和普通索引idx_reocrd_no（基于no字段）。

# ClickHouse
## 安装
curl -O 'https://builds.clickhouse.com/master/macos/clickhouse' && chmod a+x ./clickhouse
./clickhouse client -h 192.168.2.143 --port 8123 -u default --password ethicall --database rpa

# Redis
一天是 86400 秒

## TTL
Time To Live: 生存时间
键不存在或未设置过期时间，则该命令返回 -1
