---
title: Java
date: 2023-02-13 10:29:08
tags: Java
---

# Base
## 权限修饰符
|           |  private |  default(默认权限，不写)  | protected | public |
| :-------- | :--------:| :--: | :--: | :--: |
| 本类       |   Y      |   Y   |  Y   |  Y   |
| 同包       |          |   Y   |  Y   |  Y   |
| 子类       |          |       |  Y   |  Y   |
| 所有类     |          |       |      |  Y   |


## 工具类/方法
### StringUtils
isNotBlank 
StringUtils.isNotBlank(" ") = false

isNotEmpty
StringUtils.isNotEmpty(" ") = true

# Doc
## 数据类型
基本数据类型
- 整型 int x = 1
- 浮点型 float a = 3.14
- 字符类型 char zh = "中"
- 布尔类型 boolean b1 = true

引用类型
- 字符串 String s = "hello"
    final修饰符，常量
- 数组 int[] a = new int[]{1,2} , 简写 int[] a = {1,2}