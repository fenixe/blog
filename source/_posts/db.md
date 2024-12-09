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
## doc
### 创建库
create schema terminal;

### 更新表
```sql
ALTER TABLE terminal
ADD COLUMN customer_code VARCHAR(50) NOT NULL DEFAULT '' COMMENT '客户编码';
```

### 删除表唯一约束
```
ALTER TABLE goods_coupon
DROP INDEX uniq_name;
```

### 删除表内数据
empty table是清空表里的数据
truncate table是删除表,然后再创建这张表 
意义:对于主索引自动增加的情况, empty清表后, 新添加的行数据依然在上次的值上增加。而truncate则会重新从1开始

```sql
delete
from ad_group_whitelist
where ad_group_id = 38;
```

### 排序
降序：order by id desc
升序：order by id asc

## 事务
更新表无法提交
``` sql
ALTER TABLE biz_upload_record
MODIFY COLUMN no varchar(20) NOT NULL DEFAULT '' COMMENT '号';
ALTER TABLE biz_upload_record
MODIFY COLUMN result_file varchar(2000) NOT NULL DEFAULT '' COMMENT '解析后的文件,多个文件逗号连接';

-- 排查
SELECT * FROM INFORMATION_SCHEMA.INNODB_TRX;
SELECT * FROM INFORMATION_SCHEMA.PROCESSLIST WHERE ID = 2820630;
```

COMMAND = Sleep 表示该连接当前处于空闲状态，正在等待新的命令或查询。这通常发生在客户端与数据库服务器之间的连接已经建立，但当前没有任何活动的查询正在执行的情况下。


## docker
docker run --name mysql -e MYSQL_ROOT_PASSWORD=123456 -p 3306:3306 -d mysql:latest

docker run -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql

### 登录
```bash
# 帮助
$ mysql --help

# 登录
$ mysql -u root -p
123456

# 显示数据库列表
mysql> SHOW DATABASES;

# 默认模式
mysql> select @@sql_mode;
ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION

# 改为work，少一个 NO_AUTO_CREATE_USER
mysql> SET GLOBAL sql_mode = 'STRICT_TRANS_TABLES,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';
```

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


在 SQL 中，KEY idx_logis_detail_time (time) USING BTREE 是一个用于定义索引的语法，通常出现在创建或修改表的语句中，特别是在 MySQL 数据库中。让我们逐步解析这段语句：
KEY：
在 MySQL 中，KEY 是 INDEX 的同义词，用于定义一个索引。索引是数据库中用于加速数据检索的结构。
idx_logis_detail_time：
这是索引的名称。为索引命名有助于在数据库管理和优化时识别和引用它。通常，索引名称会反映它所作用的列或其用途。

(time)：
这是索引所作用的列名。在这个例子中，索引是基于 time 列创建的。索引会加速对 time 列的查询操作，尤其是在 WHERE 子句中使用 time 进行过滤时。
USING BTREE：
这指定了索引的类型。在 MySQL 中，BTREE 是默认的索引类型，适用于大多数情况。B-tree 索引适合用于范围查询、排序和等值查询。
B-tree 索引通过维护一个平衡树结构来加速数据检索，通常在处理大量数据时表现良好。

使用场景
查询优化：创建索引的主要目的是提高查询性能。对于频繁在 WHERE 子句中使用的列，创建索引可以显著减少查询时间。
排序和分组：如果查询中涉及对 time 列的排序或分组，B-tree 索引也能提高效率。
注意事项
索引开销：虽然索引可以加速查询，但它们也会增加写操作（如 INSERT、UPDATE、DELETE）的开销，因为数据库需要维护索引结构。
选择性：索引在高选择性列上效果最好，即列中不同值的数量较多。对于低选择性列（如布尔值），索引的效果可能不明显。
存储空间：索引会占用额外的存储空间，因此在创建索引时需要权衡性能提升和存储开销。

## sql脚本的导入导出
导入：navicat中，点击库，右击，运行SQL文件。
导出：navicat中，点击表，右击，导出sql文件。

## 其他
报错：Duplicate entry '6760391' for key 'uniq_ethno' 
违反了数据库中定义的唯一性约束

# ClickHouse
## 安装
curl -O 'https://builds.clickhouse.com/master/macos/clickhouse' && chmod a+x ./clickhouse
./clickhouse client -h 192.168.2.143 --port 8123 -u default --password ethicall --database rpa

# Redis
一天是 86400 秒

## TTL
Time To Live: 生存时间
键不存在或未设置过期时间，则该命令返回 -1

## 支持的存储类型
1. Strings（字符串）
String 是Redis中最基本的类型，它可以包含任何形式的数据，比如文本数据、数字或者是二进制数据，字符串类型的值最大能支持512MB。
2. Lists（列表）
Redis的List是简单的字符串列表，它按照插入顺序排序。你可以在列表的头部或尾部添加元素，这使得List特别适合实现如消息队列等功能。
3. Sets（集合）
Sets是字符串的集合，不允许有重复的成员。Redis中的Sets是无序的，你可以非常快速地进行添加、删除、查找操作，还可以进行集合之间的操作，如并集、交集、差集。
4. Sorted Sets（有序集合）
Sorted Sets也是字符串的集合，但每个字符串元素都关联了一个称为score的浮点数值，能够根据这个score进行元素的全局排序。这允许你进行快速的元素插入和删除，并能取得一个范围的元素列表。
5. Hashes（哈希）
Hashes是field-value（字段-值）对的集合，是字符串字段和字符串值之间的映射。适合用于存储对象。
6. Bitmaps（位图）
Bitmap实际上是字符串类型，它通过提供二进制位存取操作的接口来进行高效的位级操作。
7. HyperLogLogs（基数统计类型）
HyperLogLog是用于进行基数统计的算法，Redis对这个算法做了高度优化，能在非常小的空间内进行非常大数量的唯一元素计数。
8. Streams（流）
Redis Streams是Redis 5.0引入的新的数据类型，它可以存储多个键值对的序列，这些键值对被称为消息。它是构建消息队列、日志应用非常有用的一种数据类型。
9. Geospatial indexes（地理空间索引）
Redis提供的Geospatial是一种数据类型，支持存储地理位置信息并执行诸如计算两个地点之间距离、查找在给定范围内的地点等操作。
每种数据类型针对不同的应用场景和需求有着不同的命令和特性，使得Redis成为一种非常灵活的内存存储系统，适用于多种不同场景的数据管理和分析任务。

## 插入
stringRedisTemplate.opsForList().leftPush("myList", "Hello");
leftPush方法是opsForList()返回的操作类中的一个方法，用于将一个或多个值插入到列表的头部。如果列表不存在，一个新的列表会被创建出来，之后再进行推送操作。这个方法的命名中的"left"意味着插入操作是在列表的左端执行，相对地，还有一个rightPush方法用于在列表的右端插入元素。

stringRedisTemplate.opsForList().leftPushAll("myList", messages);

# 其他
## 存储内存
SQLite 20万条记录，4个字段，每个字段最多8个长度字符，大概需要多少内存？
4 个字段 * 8 个字符 = 32字节
200000 * 32 = 6400000 字节，约为6.4M
SQLite 数据库的大小会比纯数据大小大一些，但不会大很多。对于 20 万条记录和简单的结构，数据库文件可能会在 10 MB 到 20 MB 之间，具体取决于索引和其他数据库配置。
