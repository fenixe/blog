---
title: sql
date: 2023-04-20 17:06:23
tags:
---

# Base
## tinyint
占用 1 个字节（8 位）
取值范围
有符号 (SIGNED，默认) TINYINT：取值范围是 -128 到 127。
无符号 (UNSIGNED) TINYINT：取值范围是 0 到 255。

TINYINT(1) 中的 (1) 仅仅是一个显示宽度提示，不影响实际存储的数值范围。存入 10，并且取出来的值仍然是 10。

显示宽度在某些情况下可以与 ZEROFILL 一起使用，来在显示时填充零。例如，TINYINT(2) ZEROFILL 会将值 5 显示为 05。

## mysql 中 字段的 type值，int 与 bigint 的区别
在 MySQL 中，int 和 bigint 都是整数类型，但它们的区别在于所占用的存储空间大小和能够表示的范围。

int 是 MySQL 中常用的整数类型，占用 4 个字节(32位)，可以表示的范围是从 -2147483648 到 2147483647，即约 -21 亿到 21 亿之间的整数。
有符号 (SIGNED) INT：取值范围是 -2,147,483,648 到 2,147,483,647。
无符号 (UNSIGNED) INT：取值范围是 0 到 4,294,967,295。

bigint 是 MySQL 中更大的整数类型，占用 8 个字节，可以表示的范围是从 -9223372036854775808 到 9223372036854775807，即约 -922 万亿到 922 万亿之间的整数。

因此，如果您需要存储较大的整数，或者需要确保整数类型的数值不会超出范围，可以使用 bigint 类型。但是，需要注意的是，bigint 类型所占用的存储空间更大，可能会占用更多的磁盘空间，并且在进行查询和排序时可能会比 int 类型更慢。因此，在选择数据类型时需要根据具体的场景和需求进行权衡和选择。

## varchar
VARCHAR(255)：这是一个常见的选择，因为它在大多数情况下足够使用，并且只需要一个字节的长度前缀。
VARCHAR(256)：如果你确实需要存储超过 255 个字符的内容，那么选择 VARCHAR(256) 是合理的，但需要注意它会使用两个字节的长度前缀。

## 可控长度
```
在 MySQL 中，除了 `VARCHAR` 之外，还有其他几种数据类型也可以控制长度。以下是一些常见的数据类型及其长度控制方式：

### 字符串类型
1. **CHAR(n)**: 固定长度字符串。`n` 表示字符串的长度，范围是 0 到 255。例如，`CHAR(10)` 表示一个固定长度为 10 的字符串，不足的部分会用空格填充。

2. **VARCHAR(n)**: 可变长度字符串。`n` 表示字符串的最大长度，范围是 0 到 65535。例如，`VARCHAR(255)` 表示一个最大长度为 255 的字符串。

3. **TEXT** 类型及其变种:
   - **TINYTEXT**: 最大长度 255 字节。
   - **TEXT**: 最大长度 65,535 字节。
   - **MEDIUMTEXT**: 最大长度 16,777,215 字节。
   - **LONGTEXT**: 最大长度 4,294,967,295 字节。

### 数值类型
虽然数值类型的长度定义主要用于显示宽度，但在某些情况下也可以控制长度：

1. **DECIMAL(M, D)**: 定点数。`M` 表示总位数，`D` 表示小数位数。例如，`DECIMAL(5, 2)` 表示一个总位数为 5，小数位数为 2 的定点数。

2. **FLOAT(M, D)** 和 **DOUBLE(M, D)**: 浮点数。`M` 表示总位数，`D` 表示小数位数。例如，`FLOAT(7, 4)` 表示一个总位数为 7，小数位数为 4 的浮点数。

### 日期和时间类型
日期和时间类型通常不直接控制长度，但可以通过格式化来控制显示长度：

1. **DATE**: 存储日期值，格式为 `YYYY-MM-DD`。
2. **DATETIME**: 存储日期和时间值，格式为 `YYYY-MM-DD HH:MM:SS`。
3. **TIMESTAMP**: 存储时间戳，格式为 `YYYY-MM-DD HH:MM:SS`。
4. **TIME**: 存储时间值，格式为 `HH:MM:SS`。
5. **YEAR**: 存储年份值，格式为 `YYYY`。

### 枚举和集合类型
1. **ENUM('value1', 'value2', ...)**: 枚举类型，存储一个从预定义值列表中选择的单一值。
2. **SET('value1', 'value2', ...)**: 集合类型，存储一个从预定义值列表中选择的多个值的组合。

### 二进制类型
1. **BINARY(n)**: 固定长度二进制字符串。`n` 表示字符串的长度。
2. **VARBINARY(n)**: 可变长度二进制字符串。`n` 表示字符串的最大长度。

这些数据类型在定义时可以通过指定长度来控制存储和显示的格式。选择合适的数据类型和长度可以优化数据库的性能和存储效率。
```

# 表名
收货地址：user_delivery_addresses
品牌公司：BrandCompany

# Doc
## 数据类型
decimal：表示定点数
存储精确的数值，比如金融数据，其中需要精确的小数点及小数点后的数值。这与float或double的浮点数类型不同，后者可能会引入舍入误差。

## 索引
`KEY` 关键字用于定义索引。索引是一种数据库对象，用于提高查询速度。索引可以显著提高查询性能，特别是在大表上。
KEY 是 INDEX 的同义词，用于创建索引。
idx_user_username
当你在 username 列上创建索引时，数据库会创建一个数据结构（通常是 B-tree 或其他类型的树），以便更快地查找、插入、更新和删除基于 order_no 列的记录。

## 查询某字段有几种值
SELECT DISTINCT column_name
FROM table_name;

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
right join : 返回包括右表中的所有记录和左表中满足连接条件的记录。如果左表中没有匹配的记录，结果集中的左表字段将包含 NULL。

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

## 增
### 两种情况
```sql
`usage_type` tinyint(1) NOT NULL DEFAULT '1' COMMENT '使用方式：1-指定开始结束时间，2-指定领取后有效期'
`usage_start_time` datetime DEFAULT '0000-00-00 00:00:00' COMMENT '惠票使用开始时间',
`usage_end_time` datetime DEFAULT '0000-00-00 00:00:00' COMMENT '惠票使用结束时间',
`usage_valid_days` int(3) DEFAULT '0' COMMENT '领取后有效期天数',
```

### 增多条
```sql
INSERT INTO `area_config` (`province_id`, `support_type`, `init_kg`, `init_price`, `add_kg`, `add_price`, `create_time`) VALUES
(13, 1, 1, 12, 1, 8, '2024-08-15 15:00:00'),
(29, 1, 1, 12, 1, 8, '2024-08-15 15:00:00'),
```

## 查
```sql
SELECT * FROM user_data WHERE no = '7997119' OR no = '8021178'
```
### 总数
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

### 查ID后
```sql
SELECT * FROM store
WHERE keyword IS NOT NULL AND keyword <> '' AND status = 1 AND id >= 5
ORDER BY id ASC
LIMIT 2;
```

### 计数一次
```sql
SELECT COUNT(DISTINCT t.id)
FROM terminal_svk t
INNER JOIN baidu_location b ON t.id = b.pid;
```

### 时间范围
```sql
SELECT NOW() - INTERVAL 30 DAY;
```

### 过期时间记录
```sql
-- 只需要传一个 9999
UPDATE ad_content
SET status = 0
WHERE expired_time IS NOT NULL
  AND expired_time != '0000-00-00 00:00:00'
  AND expired_time < NOW();
```

### 查询某列去重
```sql
SELECT DISTINCT business
FROM baidu_coord;
```

### 英文逗号隔开的字段查询
```sql
select * from config where status = 1 and support_type = 1 and FIND_IN_SET(#{provinceId}, province_ids) limit 1
```

### 最大最小
```sql
select max(id) from l
select min(id) from l
```

### 总数
选择哪种 SQL 查询取决于你具体的需求：

1. **`SELECT COUNT(DISTINCT o.id) AS total_count FROM order_info o`**:
   - **用途**: 这个查询用于计算 `order_info` 表中唯一 `id` 的数量。如果 `id` 字段可能包含重复值，并且你只想计算唯一的订单数量，这个查询是合适的。
   - **性能**: 由于需要去重，性能可能会比简单的 `COUNT(*)` 查询稍差，特别是在 `id` 字段上没有索引的情况下。

2. **`SELECT COUNT(*) FROM order_info o`**:
   - **用途**: 这个查询用于计算 `order_info` 表中的总行数。如果你只需要知道表中的总记录数，而不关心是否有重复的 `id`，这个查询是合适的。
   - **性能**: 这个查询通常比 `COUNT(DISTINCT o.id)` 更快，因为它不需要去重操作。数据库只需要扫描表中的所有行并计数。

### 选择依据
- **如果你需要计算唯一订单的数量**（即 `id` 字段可能有重复值），使用 `COUNT(DISTINCT o.id)`。
- **如果你只需要计算表中的总行数**，使用 `COUNT(*)`。

```sql
-- 在这种情况下，使用 COUNT(*) 也是可以的，但需要确保查询的逻辑与原始查询保持一致。由于原始查询中使用了 GROUP BY，我们需要在计算总条数时保留分组逻辑。
SELECT
    COUNT(DISTINCT o.order_no) AS total_count
FROM
    order_info o

SELECT
    COUNT(*) AS total_count
FROM (
    SELECT
        o.id
    FROM
        order_info o
    GROUP BY
        o.order_no
) AS subquery;
```

### 不要用 JSON_ARRAYAGG 会导致崩溃
```sql
SELECT
    o.id,
    JSON_ARRAYAGG(
        JSON_OBJECT(
            'item_id', oi.id
        )
    ) AS orderItemsStr
FROM
    order_info o
```
```java
// 接收 json_arrayagg
response.setOrderItems(JSONArray.parseArray(response.getOrderItemsStr(), OrderInfoItemBgDetailResponse.class));
response.setOrderItemsStr("");
```

### 合并查询/联合查询
- 去重: 默认情况下，UNION 会去除重复的行。如果你想保留所有重复的行，可以使用 UNION ALL。
- 列数和数据类型: 所有参与 UNION 的查询必须有相同数量的列，并且相应列的数据类型必须兼容。
- 排序: 如果需要对结果进行排序，可以在最后一个 SELECT 语句之后使用 ORDER BY。注意，ORDER BY 只能应用于整个结果集，而不是单个查询。
```sql
SELECT column1, column2 FROM table1
UNION
SELECT column1, column2 FROM table2;

-- 保留重复的行
SELECT name, department FROM employees
UNION ALL
SELECT name, department FROM managers;

```


## update更新
把store表中的keyword字段值为“a”更改为“b”
```sql
UPDATE store
SET keyword = 'b'
WHERE keyword = 'a';
```

更新id范围内的记录
```sql
UPDATE baidu_coord
SET business = 'olm20mg7t'
WHERE id BETWEEN 182811 AND 183085;
```

## 更新comment
```sql
ALTER TABLE baidu_coord
MODIFY COLUMN type tinyint(1) NOT NULL DEFAULT '1' COMMENT '类型：1-商品，2-活动，3-惠票';

ALTER TABLE biz_upload_record
MODIFY COLUMN eth_no varchar(24) NOT NULL DEFAULT '' COMMENT '医时号';
```

### null值处理
```sql
UPDATE terminal_svk t
INNER JOIN store s ON t.`name` = s.`name` AND s.`status` = 2
INNER JOIN baidu_location b ON s.sub_id = b.id
SET t.`status` = 3, 
    t.coord = s.coord, 
    t.sub_id = s.sub_id, 
    t.tel = IFNULL(t.tel, b.tel);
```
### 空字符串处理
```sql
UPDATE terminal_temp t
INNER JOIN baidu_location_temp b ON t.sub_id = b.id
SET t.`status` = 3, 
    t.tel = CASE WHEN t.tel = '' THEN b.tel ELSE t.tel END;
```

## 删除表字段
```sql
ALTER TABLE logistics_detail
DROP COLUMN order_no;
```

## 删除记录
```sql
delete
from terminal
where id > 43550
```

## 同步数据
```sql
-- 如果遇到eth_no已经存在，而且设置了 UNIQUE KEY `uni_user_eth_no` (`eth_no`) 。一个都不会插入成功。
INSERT INTO user_data (eth_no,create_time,level)
SELECT eth_no,add_time,0 FROM ma_user;
```

## 修改表配置
```sql
SELECT @@sql_mode;

set sql_mode='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';
```