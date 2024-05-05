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

# 类
数组内是相同的数据类型，类内部是多样的数据类型
## 实例/对象（Instance/Object）

## 权限修饰符
|           |  private |  default(默认权限，不写)  | protected | public |
| :-------- | :--------:| :--: | :--: | :--: |
| 本类       |   Y      |   Y   |  Y   |  Y   |
| 同包       |          |   Y   |  Y   |  Y   |
| 子类       |          |       |  Y   |  Y   |
| 所有类     |          |       |      |  Y   |

## 构造器/构造方法
### 类型
1、默认构造函数(无参数构造函数)
2、参数化构造函数

### 默认构造函数初始值
引用类型的字段默认是null，
int类型默认值是0，
布尔类型默认值是false

## 构造函数重载
一个类可以有任何数量的参数列表不同的构造函数。编译器通过构造函数参数列表中的参数数量及其类型来区分这些构造函数。
```java
Student5(int i, String n) {
    id = i;
    name = n;
}

Student5(int i, String n, int a) {
    id = i;
    name = n;
    age = a;
}
```

## 与方法之间的区别
| Java构造函数 | Java方法 |
| :-------- | :--------:|
| 构造器用于初始化对象的状态(数据) | 方法用于暴露对象的行为 |
| 构造函数不能有返回类型 | 方法一般都有返回类型 |
| 构造函数隐式调用 | 方法要显式调用 |
| 如果没有指定任何构造函数，java编译器提供一个默认构造函数 | 在任何情况下编译器都不会提供默认的方法调用 |
| 构造函数名称必须与类名称相同 | 方法名称可以或可以不与类名称相同(随意) |

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

# 包管理工具
## Maven
### maven compile
将Java原文件编译成Class文件
1、检查项目依赖：Maven 将检查项目的配置文件 pom.xml 中声明的依赖项，并确保所需的依赖已经下载到本地 Maven 仓库中。如果依赖尚未下载，Maven 将尝试从中央仓库或其他配置的仓库中下载它们。
2、编译源代码：Maven 将查找项目中的源代码文件（通常位于 src/main/java 目录下），并将其编译成可执行的字节码文件。编译后的字节码文件通常位于 target/classes 目录下。
3、处理资源文件：Maven 还会处理项目中的资源文件（例如配置文件、属性文件等），并将其复制到编译后的输出目录中（通常也是 target/classes 目录）。

### maven package
打成jar包

### maven install
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

### pom.xml
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

### 强制安装
mvn install -U
在pom.xml文件，Maven，Reimport

## Gradle
```groovy
dependencies {
    implementation 'org.apache.commons:commons-lang3:3.11'
}
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

int number = Integer.parseInt(str);
long number = Long.parseLong(str);
```

## 数组
### 声明数组并初始化
```java
// 可以改变大小的列表
List<String> dates = new ArrayList<>(Arrays.asList("2024-04-25"));
// 方法接收一个可变参数并将其转换为一个固定大小的列表。试图调用 add 或 remove 方法，将会抛出 UnsupportedOperationException。
List<String> dates = Arrays.asList("2024-04-25", "2024-04-26");
dates.add("2024-04-26");
System.out.println(dates);
```

## 方法
### 结构
```java
// 第一层：api层
try {
    return aService.fn(req);
} catch (Exception e) {
    log.error();
    return R.fail();
}

// 第二层：service层
public class aServiceImpl implements AService {
    @Override
    public R fn(){
        try {
            b.returned();
        } catch (Exception e) {
            // 抛出一个新的运行时异常的语句
            throw new RuntimeException("除数不能为0");
        }  
    }
}

// 第三层：数据处理层
@Repository
@Slf4j
public class CRepository {
    @Transactional(rollbackFor = Exception.class)
    public R returned() throws Exception {
        throw new Exception("");
    }
}
```

### 方法参数
```java
public static List<String> getList(Integer num) {
    // 检查num是否为null
    if (num != null) {
    }
    // 你的其它逻辑
}
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

## 关键字
### final
最终的, 不可更改的。
通过限制变化，增加稳定性和安全性。
```java
// 1.修饰变量
final int i = 42; // 这个变量i不能再被赋值了

// 2.修饰方法
public class SuperClass {
    // 该方法是最终方法，不能被子类重写
    public final void show() {
        System.out.println("This is a final method.");
    }
}

// 3.修饰类
// 这个类不能被继承
public final class ConstantClass {
}
```

## 数据库
### 考虑幂等
insert ignore into

### 事务
#### @Repository
用来执行与数据库相关的操作的
```java
import org.springframework.stereotype.Repository;

@Repository
public class UserRepository {
    // ... 数据库操作方法，比如查询、插入、删除等
}
```

#### 回滚 @Transactional(rollbackFor = Exception.class)
```java
import org.springframework.transaction.annotation.Transactional;

@Transactional(rollbackFor = Exception.class)
public void updateUserData(User user) {
    // 这里可以包含多个数据库操作
    // 如果任何操作抛出Exception或其子类的异常，所有操作将被回滚
}
```
Transaction
由若干个SQL语句构成的一个操作序列，数据库系统保证在一个事务中的所有SQL要么全部执行成功，要么全部不执行，具有ACID特性：
- Atomicity：原子性
- Consistency：一致性
- Isolation：隔离性
- Durability：持久性

## 线程
``` java
private static final long REQUEST_INTERVAL_MILLIS = 1000L / 5;
// 在请求循环中等待，聚合接口5QPS限制
// for循环内会继续执行
try {
    Thread.sleep(REQUEST_INTERVAL_MILLIS);
} catch (InterruptedException ie) {
    Thread.currentThread().interrupt();
}
```

## http请求
### RestTemplate
```java
// 负载均衡
@LoadBalanced
@Bean
public RestTemplate loadBalanced1() {
    return new RestTemplate();
}

// 默认优先选择 
@Primary
@Bean
public RestTemplate restTemplate() {
    return new RestTemplate();
}
```

#### get请求
``` java
import com.alibaba.fastjson.JSONObject;
import lombok.extern.slf4j.Slf4j;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.*;
import org.springframework.stereotype.Component;
import org.springframework.web.client.RestTemplate;

@Slf4j
@Component
public class InnerHttpRequestUtils {
    @Autowired
    private RestTemplate restTemplate;

    public JSONObject get(String url) {
        try {
            ResponseEntity<JSONObject> ret = restTemplate.getForEntity(url, JSONObject.class);
            log.info("http get ret: {}", ret);
            if (ret.getStatusCode().equals(HttpStatus.OK)) {
                log.info("http get ret body: {}", ret.getBody());
                return ret.getBody();
            } else {
                throw new RuntimeException("调用服务失败");
            }
        } catch (RuntimeException e) {
            log.error("调用服务失败", e);
            return null;
        }
    }
}
```

## Redis
### 存
```java
import org.springframework.data.redis.core.StringRedisTemplate;
@Autowired
private StringRedisTemplate stringRedisTemplate;
String key = String.format(RedisKeyConsts.HOLIDAY_CACHE, day);
stringRedisTemplate.opsForValue().set(key, "1", 50, TimeUnit.DAYS);
String t = stringRedisTemplate.opsForValue().get(cacheKey);
// 检查键 "key" 是否存在, 返回 boolean
stringRedisTemplate.hasKey(ey);
```

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

### 由Spring管理，@Configuration注解定义的 bean
``` java
@Data
@Configuration
@ConfigurationProperties(prefix = "a.b")
public class AProperties {
```

### service中使用
```java
// 方式一：推荐
// 确保被注入的对象在构造后就不可改变，和@Autowired注解相比，它在编译时就能检查到依赖解决的问题。
// 对于具有很多依赖的类，构造函数注入可能会产生过长的参数列表，这可能是一个需要考虑的问题。
@AllArgsConstructor
public class VacationsService {
    private final AProperties aProperties;
}

// 方式二：
@Autowired
private AProperties aProperties;

// 方式三：
import org.springframework.cloud.context.config.annotation.RefreshScope;
@Data
@Component
@RefreshScope
public class AliOssConfig {
    @Value("${a.b}")
    private String a;
}

```

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

# 注释
## Spring注解
@Component，@Service，@Repository，@Controller，@Configuration等注解定义的bean
### @Autowired
Spring 会在上下文中自动查找匹配的依赖对象，并将其注入到被标注的字段、构造方法或者方法参数中。
不推荐：https://stackoverflow.com/questions/39890849/what-exactly-is-field-injection-and-how-to-avoid-it
推荐：构造器注入（它强制依赖在对象创建时就必须提供，使得类的依赖关系更加明显，也更容易实现不可变性和进行单元测试。）

## Lombok库注解
### @Data
自动生成toString、equals、hashCode、getter和setter方法
### @AllArgsConstructor
自动生成一个全参数构造器。会自动拥有一个构造函数，这个构造函数包含了该类中的所有字段作为参数，从而避免手动编写繁琐的构造器代码。
```java
import lombok.AllArgsConstructor;
@AllArgsConstructor
public class ExampleClass {
    private int fieldA;
    private String fieldB;
    // 其他字段...
}
// Lombok会为ExampleClass自动生成如下构造器：
public ExampleClass(int fieldA, String fieldB /* 其他字段... */) {
    this.fieldA = fieldA;
    this.fieldB = fieldB;
    // 其他字段的初始化...
}
// 在实例化ExampleClass对象时，传入所有必需的参数：
ExampleClass example = new ExampleClass(42, "The answer");
```

注意：@Value注入会失效，原因时因为@Value注解是通过对象的set方法赋值的，构造方法的执行还在set方法之前，所以在构造方法中使用变量会变量为null。

### @RequiredArgsConstructor
仅为那些被标注为@NonNull或者是final的字段生成构造函数。

### @NoArgsConstructor
生成无参构造函数。
如果你不手动提供构造方法，编译器会默认生成一个无参构造方法。但是，如果你手动提供了带参构造方法，编译器就不再生成无参构造方法。@NoArgsConstructor 解决了这个问题，它会在编译时生成一个无参构造方法，确保你的类可以在没有提供参数的情况下实例化。

## @Id
声明一个属性将映射到数据库主键的字段
数据库主键，指的是一个列或多列的组合，其值能唯一地标识表中的每一行

## @GeneratedValue
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

## @Pattern
对一个字符串类型的字段或参数进行验证，以确保它符合指定的正则表达式模式
需要将一个字符串类型的正则表达式模式作为参数传递给它
```java
@Pattern(message = "手机号格式不对", regexp = "^[1-9][0-9]{10}$")
private String mobile;
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

```xml
select * from holiday_record where query_date in
<foreach collection="days" item="day" open="(" separator="," close=")">
    #{day}
</foreach>
```

### 事务回滚
``` java
import org.springframework.transaction.annotation.Transactional;
import org.springframework.transaction.interceptor.TransactionAspectSupport;
@Transactional //方法上
TransactionAspectSupport.currentTransactionStatus().setRollbackOnly();
```

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

# FeignClient
FeignClient是Spring Cloud中的一个非常强大的工具，其目的在于简化微服务之间的HTTP调用。

特性：
声明式的客户端：你可以通过Java接口以及注解来声明一个远程服务调用的客户端，而无需实现该接口。Feign会自动为你提供实现。
简单的注解用法：使用Feign时，你只需要少量的注解，比如@FeignClient。在接口的方法中，你还可以使用Spring MVC的注解，如@RequestMapping，@PathVariable，@RequestParam等，来定义请求的URL、请求方法、参数等。
集成了Ribbon和Hystrix：Feign自然地和Spring Cloud其他组件集成，包括服务发现（Eureka）、负载均衡（Ribbon）以及断路器（Hystrix）。这意味着你可以非常容易地实现服务的自动发现和调用的容错处理。
自动编解码支持：Feign支持自动请求编码和响应解码，使得你可以直接在接口方法中使用Java对象作为参数和返回类型，Feign会自动将它们转换成HTTP请求体和从响应体中解析出结果。

``` java
@FeignClient(name = "user-service", fallback = UserFallback.class)
public interface UserServiceClient {
    @RequestMapping(value = "/users/{id}", method = RequestMethod.GET)
    User getUserById(@PathVariable("id") Long id);
}
```

# Swagger
http://localhost:8080/doc.html

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

## idea maven工程的module的Language Level总是自动变到5
``` xml
<properties>
    <maven.compiler.source>8</maven.compiler.source>
    <maven.compiler.target>8</maven.compiler.target>
</properties>
```