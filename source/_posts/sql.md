---
title: sql
date: 2023-04-20 17:06:23
tags:
---

# Base
## mysql 中 字段的 type值，int 与 bigint 的区别
在 MySQL 中，int 和 bigint 都是整数类型，但它们的区别在于所占用的存储空间大小和能够表示的范围。

int 是 MySQL 中常用的整数类型，占用 4 个字节，可以表示的范围是从 -2147483648 到 2147483647，即约 -21 亿到 21 亿之间的整数。

bigint 是 MySQL 中更大的整数类型，占用 8 个字节，可以表示的范围是从 -9223372036854775808 到 9223372036854775807，即约 -922 万亿到 922 万亿之间的整数。

因此，如果您需要存储较大的整数，或者需要确保整数类型的数值不会超出范围，可以使用 bigint 类型。但是，需要注意的是，bigint 类型所占用的存储空间更大，可能会占用更多的磁盘空间，并且在进行查询和排序时可能会比 int 类型更慢。因此，在选择数据类型时需要根据具体的场景和需求进行权衡和选择。

# Doc
## 查询某字段有几种值
SELECT DISTINCT column_name FROM table_name;

## 命令行导入sql脚本
mysql -h 192.168.2.229 -u dev -p -P 3306
mysql> USE database_name
mysql> SOURCE /path/to/file.sql;

## 排序
DESC 代表降序排列
ASC 代表升序排列

## 字段
### 删除表中无用
```sql
ALTER TABLE dev_release_version DROP COLUMN client_ids, DROP COLUMN update_status;
```

### 添加
```sql
ALTER TABLE dev_release_version ADD COLUMN priority INT DEFAULT 10;

ALTER TABLE dev_project ADD plan_hours DECIMAL(10,1) COMMENT '预估工时';

ALTER TABLE dev_project ADD plan_str VARCHAR(255) COMMENT '预估工时';
```