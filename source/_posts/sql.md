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
## 数据类型
decimal：表示定点数
存储精确的数值，比如金融数据，其中需要精确的小数点及小数点后的数值。这与float或double的浮点数类型不同，后者可能会引入舍入误差。

## 查询某字段有几种值
SELECT DISTINCT column_name FROM table_name;

### 多表查询
```sql
SELECT re.*
FROM role_resource r, resource re
WHERE r.resource_id = re.id
  AND r.active = 1
  AND re.active = 1
  AND r.role_id IN (2)
  AND re.pid = 0
GROUP BY re.id
ORDER BY re.weight ASC;
```
```xml
<select id="selectRoleHaveResource" resultType="AdminResource">
    select re.* from role_resource r,resource re where r.resource_id = re.id and r.active = 1 and re.active = 1 and
    r.role_id in
    <foreach collection="roleIds" open="(" item="item" separator="," close=")">
        #{item}
    </foreach>
    <if test="type != null and type != '' and type != 'all'">
        and re.type = #{type}
    </if>
    and re.pid = #{pid}
    group by re.id order by re.weight asc
</select>
```

inner join : 只返回两个表中联结字段相等的行
left join : 返回包括左表中的所有记录和右表中联结字段相等的记录

## 命令行导入sql脚本
mysql -h 192.168.2.229 -u dev -p -P 3306
mysql> USE database_name
mysql> SOURCE /path/to/file.sql;

## 排序
DESC 代表降序排列
ASC 代表升序排列

### 单表按ID降序
select * from user order by id desc;

多表用表别称

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

## 查总数
```sql
# 查询store表1000条中status=2的总数
SELECT COUNT(*)
FROM (
    SELECT * FROM store
    ORDER BY id ASC
    LIMIT 1000
) AS subquery
WHERE subquery.status = 2;
```

## 查ID后
```sql
SELECT * FROM store
WHERE keyword IS NOT NULL AND keyword <> '' AND status = 1 AND id >= 5
ORDER BY id ASC
LIMIT 2;
```

## update更新
把store表中的keyword字段值为“a”更改为“b”
```sql
UPDATE store
SET keyword = 'b'
WHERE keyword = 'a';
```

## 修改表配置
```sql
SELECT @@sql_mode;

set sql_mode='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION'
```