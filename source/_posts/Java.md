---
title: Java
date: 2023-02-13 10:29:08
tags: Java
---

# Base
## 执行命令
文件名要与类名一致，区分大小写
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```
``` zsh
# c compiler 编译器
$ javac HelloWorld.java 
$ java HelloWorld
Hello World
```
## 权限修饰符
|           |  private |  default(默认权限，不写)  | protected | public |
| :-------- | :--------:| :--: | :--: | :--: |
| 本类       |   Y      |   Y   |  Y   |  Y   |
| 同包       |          |   Y   |  Y   |  Y   |
| 子类       |          |       |  Y   |  Y   |
| 所有类     |          |       |      |  Y   |

## 数据放在内存中
数据库对应地址修改，要重新跑一下项目

## 调用类
### 调用静态方法
```java
public class MyClass {
    public static void myStaticMethod() {
        System.out.println("Hello from MyClass's static method!");
    }
}
public class MainClass {
    public static void main(String[] args) {
        MyClass.myStaticMethod(); // 直接调用静态方法
    }
}
```
### 调用非静态方法
```java
public class MyClass {
    public void myMethod() {
        System.out.println("Hello from MyClass!");
    }
}
public class MainClass {
    public static void main(String[] args) {
        MyClass myClassInstance = new MyClass();
        myClassInstance.myMethod(); // 调用 myMethod
    }
}
```

## 包管理工具
### Maven
#### maven compile
将Java原文件编译成Class文件
1、检查项目依赖：Maven 将检查项目的配置文件 pom.xml 中声明的依赖项，并确保所需的依赖已经下载到本地 Maven 仓库中。如果依赖尚未下载，Maven 将尝试从中央仓库或其他配置的仓库中下载它们。
2、编译源代码：Maven 将查找项目中的源代码文件（通常位于 src/main/java 目录下），并将其编译成可执行的字节码文件。编译后的字节码文件通常位于 target/classes 目录下。
3、处理资源文件：Maven 还会处理项目中的资源文件（例如配置文件、属性文件等），并将其复制到编译后的输出目录中（通常也是 target/classes 目录）。

#### maven package
打成jar包

#### maven install
把jar包安装到本地，执行所有的生命周期阶段（clean、compile、test、package、install）

1、清理项目：Maven 首先会清理项目目录下的生成的构建文件和目录，以确保从一个干净的状态开始构建。
2、编译源代码：Maven 将使用项目中的源代码（通常位于 src/main/java 目录下）进行编译，将源代码编译成可执行的字节码文件。
3、执行单元测试：如果项目中包含单元测试（通常位于 src/test/java 目录下），Maven 将执行这些单元测试，以验证代码的正确性。
4、打包生成可分发的格式：Maven 使用预定义的打包方式（例如 JAR、WAR、EAR 等）将项目的编译结果打包成可分发的格式。例如，对于 Java 项目，Maven 会将编译后的字节码文件打包成 JAR 文件。
5、安装到本地仓库：最后，Maven 将生成的构建结果（例如 JAR 文件）安装到本地 Maven 仓库中。本地仓库位于你计算机上的 .m2 目录中。这样，其他基于 Maven 的项目可以引用并使用你的项目作为依赖。


```xml
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-lang3</artifactId>
    <version>3.11</version>
</dependency>
```

#### pom.xml
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>org.example</groupId>
  <artifactId>demo</artifactId>
  <version>1.0-SNAPSHOT</version>
  <name>Archetype - demo</name>
  <url>http://maven.apache.org</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <encoding>UTF-8</encoding>
    <java.version>1.8</java.version>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>

  <dependencies>
    <dependency>
      <groupId>org.apache.commons</groupId>
      <artifactId>commons-lang3</artifactId>
      <version>3.11</version>
    </dependency>
  </dependencies>
</project>
```

#### 强制安装
mvn install -U
在pom.xml文件，Maven，Reimport

### Gradle
```groovy
dependencies {
    implementation 'org.apache.commons:commons-lang3:3.11'
}
```

## spring boot指定配置文件
IDEA
Run > Edit Configurations
Active Profiles:输入dev

## 工具类/方法
### StringUtils
isNotBlank 
StringUtils.isNotBlank(" ") = false

isNotEmpty
StringUtils.isNotEmpty(" ") = true

### BeanConvertUtils
BeanConvertUtils.trimBean(request);
request.name = " ki l " => request.name = "kil"

## 引入包
在 项目的 service 目录下 的 pom.xml 插入配置文件，点击刷新
``` xml
<dependency>
    <groupId>cn.eth.framework</groupId>
    <artifactId>framework-jwt</artifactId>
    <version>1.1.3.RELEASE</version>
</dependency>
```

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

### 数据类型转换
int -> Long
10 -> 10L
```java
Integer myInteger = 100;
Long myLong = myInteger.longValue();
```

## 对象
### 判断
equals() 方法接受一个对象作为参数，并返回一个布尔值，表示当前对象是否与参数对象相等。如果两个对象相等，那么 equals() 方法返回 true，否则返回 false。
默认情况下，Java 中的对象比较都是基于引用比较的，也就是说，如果没有重写 equals() 方法，那么它默认的行为就是比较两个对象的地址是否相等。

## var
10以上版本
类型推断的关键字，该关键字允许你不用显示声明变量的类型，编译器会自动根据右边表达式的返回值来推断变量的类型。

## 循环遍历
``` java
for (JsonNode jsonNode : arrayNode) {
    // 获取数组中的每个JsonNode元素，你可以按需进行操作
    String name = jsonNode.get("name").asText();
    String value = jsonNode.get("value").asText();

    // 打印获取的信息
    System.out.println("Item Name: " + name + ", Value: " + value);
}

// 最后一项
for (int i = 0; i < arr.length; i++) {
    if (i == arr.length - 1) {
        System.out.println(arr[i] + " is the last element.");
    } else {
        System.out.println(arr[i]);
    }
}
```

## 注释
### @Id
声明一个属性将映射到数据库主键的字段
数据库主键，指的是一个列或多列的组合，其值能唯一地标识表中的每一行

### @GeneratedValue
指示如何生成实体类的主键。主键是一个唯一标识实体的属性，每个实体类都必须有一个主键。
参数
- GenerationType.AUTO：让 JPA 自动选择适合数据库的主键生成策略，这是默认值。
- GenerationType.IDENTITY：使用自增长字段生成主键，通常适用于 MySQL、SQL Server 等数据库。
- GenerationType.SEQUENCE：使用序列生成主键，通常适用于 Oracle、PostgreSQL 等数据库。
- GenerationType.TABLE：使用一个特定的数据库表来存储生成的主键值。
```java
@Id
@GeneratedValue(strategy = GenerationType.IDENTITY)
private Long id;
```

### @Pattern
对一个字符串类型的字段或参数进行验证，以确保它符合指定的正则表达式模式
需要将一个字符串类型的正则表达式模式作为参数传递给它
```java
@Pattern(message = "手机号格式不对", regexp = "^[1-9][0-9]{10}$")
private String mobile;
```

## 数据库事务
Transaction
由若干个SQL语句构成的一个操作序列，数据库系统保证在一个事务中的所有SQL要么全部执行成功，要么全部不执行，具有ACID特性：
- Atomicity：原子性
- Consistency：一致性
- Isolation：隔离性
- Durability：持久性

## 处理文件
### json
```xml
<!-- 添加到你的pom.xml依赖中 -->
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.13.1</version>
</dependency>
```
```java
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.JsonNode;

import java.io.File;
import java.io.IOException;

public class JsonExample {
    public static void main(String[] args) {
        ObjectMapper mapper = new ObjectMapper();
        try {
            // 读取JSON文件并转换为JsonNode
            JsonNode rootNode = mapper.readTree(new File("path/to/your/jsonfile.json"));
            // 处理JsonNode或将其转换为POJO
            // 假设我们只是打印这个JsonNode
            System.out.println(rootNode.toString());
            // 如果需要将修改后的JsonNode写回文件
            mapper.writeValue(new File("path/to/your/output_jsonfile.json"), rootNode);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

# Example
## mapper
``` xml
<insert id="insertAdminRole">
    insert into admin_role (admin_id,role_id,create_time,update_time) VALUES
    <foreach collection="roleIds" item="item" separator=",">
        (#{adminId} ,#{item} ,#{now} ,#{now} )
    </foreach>
</insert>

<insert id="createAdmin" useGeneratedKeys="true" keyProperty="admin.id">
    insert into admin (amid,mobile,pwd,real_name,salt,add_time,dept_id,email) VALUES (#{admin.amid} ,#{admin.mobile} ,#{admin.pwd} ,#{admin.realName} ,#{admin.salt} ,#{admin.addTime} ,#{admin.deptId} ,#{admin.email} )
</insert>

<update id="updateRecord" parameterType="map">
    update biz_upload_record
    <set>
        <if test="status != null">
            status=#{status},
        </if>
        update_time=#{updateTime}
    </set>
    where id=#{id}
</update>
```

MyBatis框架中，SQL语句根据传递参数动态更改结构
```xml
<select id="selectTag" resultType="Tag">
    select * from tag
    where 1=1
    <if test="id != null">
        and id != #{id}
    </if>
    order by id desc
    limit 1
</select>
```

MyBatis foreach 查询，转化成sql指令查询
```xml
select name from tag whereid = 1 and name in
<foreach collection="names" open="(" item="item" separator="," close=")">
    #{item}
</foreach>
```
select name from tag where id = 1 and name in ('name1', 'name2', 'name3')

MyBatis, selectByPrimaryKey 方法通常是由 MyBatis 框架中的 Mapper 接口提供的，它用于根据主键（Primary Key）检索数据库中的一条记录
Bot bot = botMapper.selectByPrimaryKey(botId);
SELECT * FROM bot_table WHERE id = ?;

## service
### interface
``` java
public interface AdminService {
    R createAdmin(CreateAdmRequest request);
}
```

### implements
``` java
public class AdminServiceImpl implements AdminService {
    @Autowired
    private AdminMapper adminMapper;

    @Transactional
    public R createAdmin(CreateAdmRequest request){
        // 业务逻辑
        Admin admin = new Admin();
        admin.setName(request.getName());
        adminMapper.createAdmin(admin);
        return R.ok(GlobalRetCode.成功.code, msg: ok, data: null);
    }
}
```

## Route
``` java
public class Adm {
    @Autowired
    private AdminService adminService;

    /**
     * 创建用户
     * @param request
     * @return
     */
     @PostMapping("/user/create")
     @ApiOperation(value = "创建用户")
     @Validated
     public R createAdmin(@RequestBody CreateAdmRequest request){
        log.info(">>> 创建用户 request {}", JSON.toJSONString(request));
        try{
            // 必填基本判断：非空
            return adminService.createAdmin(request);
        } catch(Exception e){
            log.error("{}", e);
            return R.fail(GlobalRetCode.服务器内部错误.code, GlobalRetCode.服务器内部错误.name(), null);
        }
     }
}
```

# IDEA
## 替换
全局
command + shift + r
局部
command + r

## 多光标同时编辑
shift + alt + 鼠标左键

## 设置代理
Appearance & Beahvior -> System Settings -> HTTP Proxy
配置后，check 按钮

# Maven
创建项目
mvn archetype:generate -DgroupId=com.example -DartifactId=myproject -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

# Function
## Nacos
appid:
  config: 
    - ids: 1,2
      accessKeyId: LTAI5tDEY414S
``` java
public static AliOssConfig.IdConfig findItemById(String id, List<AliOssConfig.IdConfig> dataList) {
    log.info("id:{}", id);
    for (AliOssConfig.IdConfig item : dataList) {
        List<String> ids = item.getIds();
        log.info("ids{}", ids);
        if (ids.contains(id)) {
            log.info("item{}", item);
            return item;
        }
    }
    return null;
}
```

# Issues
## Java implements Serializable 什么意思
Java中的Serializable接口是一个标记接口，用于指示一个类的对象可以被序列化为字节流并在网络上传输或存储在磁盘上。一个类只需要实现Serializable接口，就可以使它的对象可序列化。
当一个类实现了Serializable接口，编写的Java代码可以使用对象输出流(ObjectOutputStream)将对象序列化为字节流，而对象输入流(ObjectInputStream)可以将字节流反序列化为原始对象。这个过程允许Java应用程序在网络上传输对象，或将对象永久存储在磁盘上以备将来使用。
需要注意的是，实现Serializable接口的类可能会存在安全风险，因为它们允许对象在网络上传输或在磁盘上存储。因此，开发人员需要小心谨慎地处理序列化和反序列化的过程，以防止对程序的安全造成潜在的威胁。

## Diamond types are not supported at this language level '7'
File->project -> Modules -> Source -> Language Leve -> 8-Lambda,type annotation etc.
File->project -> Project中 -> project Language Level -> 8-Lambda,type annotation etc.
Preferences -> Build,execution,Deployment -> Compiler -> Java Compiler

## try catch
``` java
public static void runTest() {
    try {
        System.out.println("run 1");
        try {
            System.out.println("run 2");
            // 模拟一个错误情况
            throw new Exception("这是一个测试异常");
        } catch (Exception err) {
            System.out.println("err 2" + err);
        }
        System.out.println("run 2 after");
    } catch (Exception e){
        System.out.println("err 1" + e);
    }
}
run 1
run 2
err 2java.lang.Exception: 这是一个测试异常
run 2 after
```
