---
title: Java
date: 2023-02-13 10:29:08
tags: Java
---

# Base
Java是一种强类型语言，这意味着每个变量都必须声明其类型。
## 变量
- 变量的声明和初始化
- 变量的类型
- 变量的作用域
- 常亮
  final int CONSTANT_VAR = 100;
- 变量命名规则

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

# 启动一个jar包
java -jar hellospring-0.0.1-SNAPSHOT.jar
```

## Bean
Bean简单来讲就是由Spring容器创建并托管的实例。

```java
Bean转map
Map<String, Object> param = BeanUtil.beanToMap(request);
log.info("region list param: {}", JSON.toJSONString(param));
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

## bootstrap.yaml 文件
用于以下几种情况：
1、Spring Cloud Config：当使用Spring Cloud Config时，bootstrap.yaml文件通常用于配置应用程序从配置服务器获取配置的相关信息。因为这些配置需要在应用程序启动的早期阶段加载，所以放在bootstrap.yaml中。

2、早期初始化配置：某些配置需要在应用程序启动的早期阶段加载，例如加密/解密配置、应用程序名称、环境配置等。这些配置通常放在bootstrap.yaml中。

3、分布式配置：在分布式系统中，bootstrap.yaml文件可以用于配置服务发现、配置中心等需要在应用程序启动时就加载的配置。

### 加载顺序
Spring Boot在启动时会首先加载bootstrap.yaml文件，然后再加载application.yaml文件。

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
### 基础
maven有两部分组成
服务器端，maven repo
仓库里每个 jar 包，都有唯一的id。这个id由三部分组成：group id，artifact id 和 version
maven会把下载好的 artifact 放在本地的文件夹，叫 local repo

客户端
项目中会把 jar包的id加入到自己的依赖。maven的依赖是传递的，发布本地jar包到 maven repo，自动依赖所有。

### 重新依赖
没找到方法
powerJobClient.fetchWorkflowInstanceFailPage();
~/.m2/repository/tech -> ~/.m2/repository/tech2
tech2 2024年2月28日
tech 2024年9月2日
mvn clean
刷新，Reload All Maven Projects

### 打包
``` zsh
mvn clean package -Dmaven.test.skip
```

### 创建项目
mvn archetype:generate -DgroupId=com.example -DartifactId=myproject -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

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
    <version>3.10</version>
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

### 自己的parent
``` xml
<parent>
    <artifactId>framework-dependencies</artifactId>
    <groupId>cn.eth.framework</groupId>
    <version>1.1.6.RELEASE</version>
</parent>
```

### 不使用parent
使用dependencyManagement，实现parent功能
``` xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-dependencies</artifactId>
            <version>${spring-boot.version}</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>

<!-- == -->

<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-dependencies</artifactId>
    <version>${spring-boot.version}</version>
    <relativePath/>
</parent>

<!-- 生成一个可执行的 jar包 -->
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
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

# 项目目录结构
## Domain 文件夹
存放与业务领域相关代码，如：数据传输对象
这些类的作用是提供对数据的不同视图和操作，以支持数据在不同层（例如持久层、服务层、展示层）之间的传递和转换。

## Entity
这个文件夹和domain类似，也是用于存放实体类，但可能更倾向于将其用于存放一些非业务相关的实体类。

# Doc
## 数据类型
8种基本数据类型
- 整数类型
  * byte：8位，范围从 -128 到 127
  * short：16位，范围从 -32,768 到 32,767
  * int：32位，范围从 -2^31 到 2^31-1
  * long：64位，范围从 -2^63 到 2^63-1

- 浮点类型
  * float：32位，单精度
  * double：64位，双精度

- 字符类型
  * char：16位，存储单个字符，使用Unicode编码

- 布尔类型
  * boolean: 只有两个值：true 和 false


引用类型
引用数据类型包括类、接口、数组和枚举。引用数据类型的变量存储的是对象的引用（地址），而不是对象本身。
- 字符串 String s = "hello"
    final修饰符，常量
- 数组 
```java
// 简单初始化
int[] a = {1,2} // 声明并初始化数组

// 使用 new 关键字的初始化
int[] a = new int[]{1,2} , 
int[] intArray;
intArray = new int[]{1, 2, 3}; // 可以在声明之后的任何地方初始化数组
```

引用数据类型特点
- 存储引用：引用数据类型的变量存储的是对象的引用，而不是对象本身。
- 多态性：引用数据类型支持多态性，一个接口类型的引用可以指向任何实现该接口的对象。
- 方法调用：通过引用数据类型的变量，可以调用对象的方法。

### 浮点类型
- float：32 位，单精度，范围约为 1.4E-45 到 3.4E+38。
- double：64 位，双精度，范围约为 4.9E-324 到 1.8E+308。

f 或 F 是一个后缀，用于表示一个浮点数字面量是 float 类型。默认情况下，Java 中的小数（如 0.1）被认为是 double 类型。如果你想明确表示一个数是 float 类型，就需要在数字后面加上 f 或 F。

```java
// 默认是 double 类型
double doubleNumber = 0.1;
System.out.println("Double number: " + doubleNumber);

// 明确表示为 float 类型
float floatNumber = 0.1f;
System.out.println("Float number: " + floatNumber);

Double number: 0.1
Float number: 0.1

// 精度丢失问题
0.1 + 0.2 = 0.30000000000000004
```

### 字符串
#### String 类
String 类是不可变的，这意味着一旦创建了字符串对象，它的值就不能改变。任何对字符串的修改都会创建一个新的字符串对象，而不是修改原来的对象。

#### 字符串的创建
字面量方式
```java
String str = "hello world";
```
这种方式直接在代码中使用字符串字面量。Java会在字符串池（String Pool）中查找是否已经存在相同内容的字符串对象。如果存在，则返回该对象的引用；如果不存在，则创建一个新的字符串对象并放入字符串池中。

使用 `new` 关键字
```java
String str = new String("hello world");
```
这种方式显式地创建一个新的字符串对象，不管字符串池中是否已经存在相同内容的字符串对象。

#### 字符串池（String Pool）
字符串池是Java中一个特殊的内存区域，用于存储字符串字面量。字符串池的主要目的是为了节省内存和提高性能。通过字符串池，Java可以确保相同内容的字符串字面量只存储一份。

#### 字符串的不可变性
```java
String str = "hello";
str = "world";
```
在这个例子中，str 最初引用的是内容为 "hello" 的字符串对象。当我们将 str 重新赋值为 "world" 时，实际上是创建了一个新的字符串对象 "world"，并让 str 引用这个新对象，而原来的 "hello" 对象仍然存在于字符串池中（如果没有其他引用指向它，它将被垃圾回收）。

#### 常用的字符串操作
长度：str.length()
拼接：str.concat(" world") 或 str + " world"
子字符串：str.substring(0, 5)
字符查找：str.charAt(1)
字符串比较：str.equals("hello") 或 str.equalsIgnoreCase("HELLO")
字符串替换：str.replace('h', 'H')
字符串分割：str.split(" ")
```java
// 转Integer, 两种
int number = Integer.parseInt(numberAsString);
Integer number = Integer.valueOf(numberAsString);

String dir = String.format("%s%s/%s/%s", directory, formattedDate, extensionDir, UUID.randomUUID());

// 正则匹配
input.matches("[a-zA-Z]+")
// 一个字符是否是字母
Character.isLetter(ch)

import org.apache.commons.lang.StringUtils;
String str1 = null;
String str2 = "";
String str3 = " ";
boolean isStr1Empty = StringUtils.isEmpty(str1); // true，因为str1是null
boolean isStr2Empty = StringUtils.isEmpty(str2); // true，因为str2长度为0
boolean isStr3Empty = StringUtils.isEmpty(str3); // false，因为str3包含一个空格字符

Set<String> provinceIdSet = new HashSet<>(Arrays.asList(areaConfig.getProvinceIds().split(",")));
String[] requestProvinceIds = request.getProvinceIds().split(",");
for(String id: requestProvinceIds) {
    return false;
}

// 判断一个字符串是否为 null、空字符串或仅包含空白字符。
import org.apache.commons.lang3.StringUtils;
StringUtils.isBlank(request.getDepartmentIds())

// 字符只能是数字
String No = "6867576";
boolean isNumeric = StringUtils.isNumeric(No);
```

### int类型
除法向下取整

基本数据类型int的比较，通常使用==操作符。
Integer类的equals方法确实可以用来比较两个Integer对象的值是否相等。



### 布尔类型
boolean是Java的基本数据类型，它只有两个可能的值：true或false。它不是一个对象，它的内存占用也更小，因为它直接存储值。
```java
boolean exists = true; // 或者 false
```
Boolean是boolean的包装类。它是java.lang.Boolean类的一个实例，这个类提供了很多方法，例如将字符串转换成布尔值。Boolean对象可以是null，true或false。
```java
Boolean exists = Boolean.TRUE;  // 或者 Boolean.FALSE 或者 null
```


### 数据类型转换
int -> Long
10 -> 10L
```java
Integer myInteger = 100;
Long myLong = myInteger.longValue();

int number = Integer.parseInt(str);
long number = Long.parseLong(str);

// 转换到固定类型
GoodsCouponBgListResponse row = BeanUtil.copyProperties(coupon, GoodsCouponBgListResponse.class);
// 忽略id，name
BeanUtil.copyProperties(request.getTicketInfo(), existingCouponTicket, "id", "name");

BeanUtil.copyProperties(coupon, couponRes);
GoodsCouponBgListResponse couponRes = new GoodsCouponBgListResponse();
```

## 引用数据类型
### 类（Classes）
#### BigDecimal 高精度计算类
位于 java.math 包中。
BigDecimal: 是一个不可变的、任意精度的有符号十进制数。高精度，比如货币计算时。
sql定义字段：`longitude` decimal(10,7)
表示：最多可以存储10位数字，其中7位是小数部分。
通常支持任意位数的小数部分

```java
// 创建
new BigDecimal("1.1")
BigDecimal.valueOf(2)

BigDecimal goodsWeight = new BigDecimal("1.1");
Long goodsNum = 1L;
BigDecimal totalWeight = goodsWeight.multiply(new BigDecimal(goodsNum)); // 乘法
System.out.println(totalWeight);

Integer initKg = 1;
BigDecimal initPrice = new BigDecimal("6");
// 比较
System.out.println(totalWeight.compareTo(new BigDecimal(initKg)) > 0);

BigDecimal exceedWeight = totalWeight.subtract(BigDecimal.valueOf(initKg)); // 减法
System.out.println(exceedWeight);

BigDecimal add = goodsWeight.add(new BigDecimal("1")); // 加法
System.out.println(add);

// 除法
BigDecimal quotient = bd1.divide(bd2, BigDecimal.ROUND_HALF_UP);
System.out.println("Quotient: " + quotient);
```

#### compareTo
```java
compareTo 方法用于比较两个 BigDecimal 对象的大小。
如果调用对象小于参数对象，compareTo 方法返回 -1。
如果调用对象等于参数对象，compareTo 方法返回 0。
如果调用对象大于参数对象，compareTo 方法返回 1。
```

#### 向下取整
```java
NumberUtil.round(9.9, 0, RoundingMode.DOWN).longValue();
```
NumberUtil.round 是一个静态方法，用于对数字进行舍入。
参数 9.9 是要舍入的数字。
参数 0 表示舍入到小数点后0位（即整数部分）。
RoundingMode.DOWN 表示向下舍入（即截断小数部分）。

#### 向上取整
```java
// 快递费
BigDecimal exceedWeight = new BigDecimal("24.2");
BigDecimal exceedWeightCopies = exceedWeight.divide(BigDecimal.valueOf(2), 0, BigDecimal.ROUND_UP); // 除法
System.out.println(exceedWeightCopies);
```

## 数组
subList(start, end)取得的是下标为start到end-1的元素,不包含下标为end的元素.
### 声明数组并初始化
```java
// 空数组
Collections.emptyList()
// 只有一个元素的数组
Collections.singletonList(Enum.SUC)
CollectionUtils.isEmpty(standardIds)

// 固定大小的数组
String[] datas
User[] users
System.out.println(Arrays.toString(data));

// 可以改变大小的列表（集合）
List<String> dates = new ArrayList<>(Arrays.asList("2024-04-25"));
// 方法接收一个可变参数并将其转换为一个固定大小的列表。试图调用 add 或 remove 方法，将会抛出 UnsupportedOperationException。
List<String> dates = Arrays.asList("2024-04-25", "2024-04-26");
dates.add("2024-04-26");
System.out.println(dates);
```

### asList
Arrays.asList() 是一个 Java 的静态方法，它可以把一个数组或者多个参数转换成一个 List 集合。

### 数据处理
```java
// 提取ids
List<Integer> ids = list.stream().map(ResClass::getId).collect(Collectors.toList());
List<Long> pLongList = Arrays.stream(pIds.split(",")).map(Long::parseLong).collect(Collectors.toList());

// 按照父元素，进行分组，一对多
Map<Integer, List<Tag>> tagMap = tags.stream()
                .collect(Collectors.groupingBy(Tag::getPid));
// groupingBy 方法接收一个函数作为参数，它将作为分组的键。
// 输出：{1=[Tag(pid=1, n=a), Tag(pid=1, n=d)], 3=[Tag(pid=3, n=b), Tag(pid=3, n=c)]}
List<String> list = Arrays.asList("a", "bb", "cc", "ddd");
Map<Integer, List<String>> map = list.stream().collect(Collectors.groupingBy(String::length));

// 一对一
Map<Long, RegionResponse> regionMap = regionList.stream().collect(Collectors.toMap(RegionResponse::getId, region -> region));
Map<Integer, User> userMap = Arrays.stream(users).collect(Collectors.toMap(User::getId, user -> user));
System.out.println(userMap.get(1));

// 筛选/过滤
List<ExpressAreaConfigCreateRequest> areaNotSupportList = reqAreaList.stream()
                .filter(o -> ExpressAreaConfig.SupportTypeEnum.不.code.equals(o.getSupportType()))
                .collect(Collectors.toList());
List<User> filterUserList = Arrays.stream(users).filter(user -> user.getId() == 3).collect(Collectors.toList());


// 是否有supportType = 0的项。
[{
"provinceIds": "14,15,16",
"supportType": 0
},{
"provinceIds": "1",
"supportType": 1
}]
boolean hasSupportTypeZero = areaConfigList.stream().anyMatch(o -> ExpressAreaConfig.SupportTypeEnum.不送达.code.equals(o.getSupportType()));

// initKg,initPrice,addKg,addPrice 相同判断
log.info("起步价：{}, 增加价：{}", request.getInitPrice(), request.getAddPrice());
log.info("起步价类型：{}, 增加价类型：{}", request.getInitPrice().getClass(), request.getAddPrice().getClass());
boolean hasSame = areaConfigList.stream()
        .peek(o -> log.info("起步价判断：{}, 增加价判断：{}", o.getInitPrice().compareTo(request.getInitPrice()) == 0, o.getAddPrice().compareTo(request.getAddPrice()) == 0))
        .anyMatch(o -> o.getInitKg().equals(request.getInitKg()) && o.getInitPrice().compareTo(request.getInitPrice()) == 0
        && o.getAddKg().equals(request.getAddKg()) && o.getAddPrice().compareTo(request.getAddPrice()) == 0);
if (hasSame) {
    return R.ok(GlobalRetCode.请求参数验证有误.code, "已存在相同配置", null);
}

// 数组转字符串，用"；"连接
List<String> goodsNames = Arrays.asList("Apple", "Banana", "Cherry");
String result = String.join(";", goodsNames);

// Set 和 List 查找：contains
// Set不允许重复 O(1)更快，List允许重复 O(n)较慢
List<String> Nos = new ArrayList<>();
Set<String> NosSet = new HashSet<>(Nos);
NosSet.contains(No)

// ids是否都在AuditRecords中
Set<String> orderAuditRecordNos = new HashSet<>();
for (OrderAuditRecord record : orderAuditRecords) {
    orderAuditRecordNos.add(record.getOrderNo());
}
for (String orderNo : orderNos) {
    if (!orderAuditRecordNos.contains(orderNo)) {
        log.info("批量审核记录不存在，订单编号：{}", orderNo);
    }
}
```

### stream操作
对数据源（如集合、数组等）进行操作
```java
// 从集合创建 Stream
List<String> list = Arrays.asList("a", "b", "c");
Stream<String> streamFromList = list.stream();

// 从数组创建 Stream
String[] array = {"a", "b", "c"};
Stream<String> streamFromArray = Arrays.stream(array);

// 使用 Stream.of 创建 Stream
Stream<String> streamOf = Stream.of("a", "b", "c");

// 找出最小的一项
int sendOutType = items.stream().map(OrderInfoItemBgDetailResponse::getSendOutType).min(Integer::compareTo).orElse(0);
```

stream操作分为中间操作（intermediate operations）和终端操作（terminal operations）。
中间操作仅仅在终端操作触发时才会执行。

- .collect(Collectors.toList()) — 收集结果到一个新的列表
- .forEach(System.out::println) — 对每个元素执行给定的操作
- .count() — 返回stream中元素的总数
- .filter() 筛选
- .map() 元素转换另一种形式
- .reduce() 组成一个结果
- .sorted() 对元素进行排序
- .anyMatch() 有一个符合
- .allMatch() 全部符合
- .noneMatch() 都不符合
- .peek() 对流中的每个元素执行一个操作（可以是获取、修改或打印等），而不影响流的整体处理流程

```java
exportTerminals.stream().map(o -> {
  o.setType();
}).collect(Collectors.toList());

// json文件转数组
List<Map<String, String>> datas = jsonRes.getDatas();
List<String> values = datas.stream()
        .flatMap(map -> map.values().stream())
        .collect(Collectors.toList());
ethNos.addAll(values);
```

### 是否在数组中
``` java
// 数组：[{name:a},{name:b}]。我现在有一个name：x，如何判断name ：x 有没有在其中中
Map<String, String> map1 = new HashMap<>();
map1.put("name", "a");
Map<String, String> map2 = new HashMap<>();
map2.put("name", "b");
List<Map<String, String>> listOfMaps = Arrays.asList(map1, map2);

String nameToCheck = "x";
boolean exists = listOfMaps.stream().anyMatch(map -> nameToCheck.equals(map.get("name")));
System.out.println("Does name exist in the array? " + exists);
```

### 数组转listResponse类型
```java
List<UserBgListResponse> rows = BeanUtil.copyToList(userInfoList, UserBgListResponse.class);
```

## 方法FN
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

### Lambda表达式
(parameters) -> expression
```java
List<String> list = Arrays.asList("apple", "orange", "banana");
// filter 方法使用了一个 Lambda 表达式来筛选以 "a" 开头的字符串
list.stream()
    .filter(s -> s.startsWith("a"))
    .forEach(System.out::println);
```

## Math
min() 方法用于返回两个参数中的最小值。
end = Math.min(0 + 3, 9) = 3

## Enum
```java
public enum StatusEnum {
    成功("1"),
    失败("2"),
    ;
    public final String code;
    StatusEnum(String code) {
        this.code = code;
    }
}
StatusEnum.成功.code
```

## 对象
```java
String str = obj.toString();

Map params = new HashMap<String, String>();
params.put("doctor_name", taskRecord.getDoctorName());
```
### 判断
equals() 方法接受一个对象作为参数，并返回一个布尔值，表示当前对象是否与参数对象相等。如果两个对象相等，那么 equals() 方法返回 true，否则返回 false。
默认情况下，Java 中的对象比较都是基于引用比较的，也就是说，如果没有重写 equals() 方法，那么它默认的行为就是比较两个对象的地址是否相等。

### JSON 转匹配类型
```java
OssStsTokenResponse ossStsTokenResponse = JSON.parseObject(JSON.toJSONString(response.get("data")), OssStsTokenResponse.class);
```

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

### 无限循环
```java
while (true) {
    // 你的代码逻辑

    // 检查是否满足终止条件
    if (检查终止条件) {
        break; // 终止循环
    }
}
int counter = 0;
while (true) {
    System.out.println("Counter: " + counter);
    counter++;

    // 当计数器达到5时终止循环
    if (counter >= 5) {
        break;
    }
}

for (;;) {
    // 执行你的代码

    // 如果满足终止条件
    if (检查终止条件) {
        break; // 跳出循环
    }
}
```

### 标签（Label）
标签可以与 break 和 continue 语句一起使用，以控制多层循环。
```java
outerLoop:
for (int n = 0; n < 5; n++) {
    for (int o = 0; o < 5; o++) {
        if (o == 3) {
            break outerLoop; // 终止外层循环
        }
        System.out.println("n = " + n + ", o = " + o);
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

## 时间
```java
import org.apache.commons.lang3.time.DateFormatUtils;
import java.util.Date;
String currentTime = DateFormatUtils.format(new Date(), "yyyy-MM-dd HH:mm:ss");
```

### 比较
- 优先使用 isAfter 方法：如果你在使用 Java 8 及以上版本，推荐使用新的日期时间 API 和 isAfter 方法。新的 API 更现代化，设计更好，代码更清晰和安全。
- 使用 after 方法：如果你使用的是旧的 Date 类，并且只需要简单的时间比较，after 方法是一个不错的选择。
- 使用 compareTo 方法：如果你需要进行复杂的比较逻辑或排序，compareTo 方法提供了更灵活的返回值，可以满足`多种`(if>0 - else if<0 - else=)需求。

### Calendar
```java
// 加一天
Calendar calendar = Calendar.getInstance();
calendar.setTime(new Date());
calendar.add(Calendar.DAY_OF_MONTH, 1);
Date tomorrow = calendar.getTime();

// 设置某天的结束时间
calendar.set(Calendar.YEAR, 2024);
calendar.set(Calendar.MONTH, Calendar.SEPTEMBER); // 注意：月份从0开始，0表示1月
calendar.set(Calendar.DAY_OF_MONTH, 30);
// 设置时间为23:59:59
calendar.set(Calendar.HOUR_OF_DAY, 23);
calendar.set(Calendar.MINUTE, 59);
calendar.set(Calendar.SECOND, 59);

// 如果是当前时间，就不需要下面这样设置了，因为 getInstance() 方法已经初始化为当前时间。
calendar.setTime(new Date());
```

## 常用类库
### Set
Set 是一种集合接口，它继承自 Collection 接口。Set 的特点是其元素是无序的，并且不允许包含重复的元素。
#### HashSet
HashSet 是最常用的 Set 实现类，基于哈希表实现。它不保证集合的迭代顺序，顺序可能与插入顺序不同，甚至可能随时间变化。
```java
Set<String> hashSet = new HashSet<>();
hashSet.add("Apple");
hashSet.add("Banana");
hashSet.add("Orange");
hashSet.add("Apple"); // 重复元素不会被添加

for (String fruit : hashSet) {
    System.out.println(fruit);
}
```

#### LinkedHashSet
LinkedHashSet 是 HashSet 的子类，具有可预知的迭代顺序。它维护一个双向链表，记录元素的插入顺序，因此迭代时会按插入顺序返回元素。
```java
Set<String> linkedHashSet = new LinkedHashSet<>();
linkedHashSet.add("Apple");
linkedHashSet.add("Banana");
linkedHashSet.add("Orange");
linkedHashSet.add("Apple"); // 重复元素不会被添加

for (String fruit : linkedHashSet) {
    System.out.println(fruit);
}
```

#### TreeSet
TreeSet 是基于红黑树实现的 Set，它保证元素的自然顺序（或根据提供的比较器排序）。TreeSet 的性能比 HashSet 稍差，但它提供了排序功能。

#### EnumSet
EnumSet 是一个专门为枚举类型设计的 Set 实现。它比其他 Set 实现更高效，但只能用于枚举类型。

#### 常用操作
- add(E e)：将指定的元素添加到集合中（如果该元素尚不存在）。
- remove(Object o)：从集合中移除指定的元素（如果存在）。
- contains(Object o)：如果集合包含指定的元素，则返回 true。
- size()：返回集合中的元素数量。
- isEmpty()：如果集合不包含任何元素，则返回 true。
- clear()：移除集合中的所有元素。
- iterator()：返回集合中元素的迭代器。

## 数据库
### 连接
```
spring.datasource.driver-class-name: com.mysql.cj.jdbc.Driver
spring.datasource.url: jdbc:mysql://127.0.0.1:3306?autoReconnect=true&useUnicode=true&characterEncoding=utf8&zeroDateTimeBehavior=convertToNull&allowMultiQueries=true&serverTimezone=Asia/Shanghai
spring.datasource.username: root
spring.datasource.password: 123
spring.datasource.druid.initial-size: 10
spring.datasource.druid.min-idle: 5
spring.datasource.druid.max-active: 20
spring.datasource.druid.max-wait: 60000
spring.datasource.druid.time-between-eviction-runs-millis: 60000
spring.datasource.druid.min-evictable-idle-time-millis: 30000
spring.datasource.druid.test-on-borrow: false
spring.datasource.druid.test-while-idle: true
spring.datasource.druid.validation-query: select 'x'
spring.datasource.druid.validation-query-timeout: 60000
```

查询是否连接成功
```java
// 方法一：JdbcTemplate
@Autowired
private JdbcTemplate jdbcTemplate;

@RequestMapping("/hello")
public String hello(@RequestParam(name = "name", defaultValue = "unknown user") String name) {
    System.out.println(smsStatus);
    System.out.println(aiUrl);

    // 为1 成功连接
    Integer result = jdbcTemplate.queryForObject("SELECT 1", Integer.class);
    System.out.println(result);
    return "Hello " + name;
}

// 方法二： JPA Repository
// 假设一个简单的实体类 User 和对应的 UserRepository。

@Entity
public class User {
    @Id
    private Long id;
    private String name;
}

import org.springframework.data.jpa.repository.JpaRepository;
public interface UserRepository extends JpaRepository<User, Long> {
}

// 在控制器中使用 UserRepository
@Autowired
private UserRepository userRepository;

long count = userRepository.count();
```

### 考虑幂等
insert ignore into

### 事务
`事务`是一组操作的集合，它是一个不可分割的工作单位，这些操作 要么同时成功，要么同时失败。

#### @Repository
用来执行与数据库相关的操作的
```java
import org.springframework.stereotype.Repository;

@Repository
public class UserRepository {
    // ... 数据库操作方法，比如查询、插入、删除等

    int i = 1/0 // 模拟抛出异常
}
```

#### 回滚 @Transactional(rollbackFor = Exception.class)
为什么在 biz 目录中使用 @Transactional
biz 目录通常包含业务逻辑层的代码，负责处理应用程序的核心业务操作。这些操作通常需要多个数据库操作来完成，因此事务管理在这里显得尤为重要。使用 @Transactional 可以确保这些操作的一致性和完整性。
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

```java
@Service
@Transactional(rollbackFor = {Exception.class, RuntimeException.class})
public class BannerBiz {

    @Resource
    private PostActivityMapper postActivityMapper;

    @Resource
    private BannerConfigMapper bannerConfigMapper;

    public void updateBanner(BannerConfigUpdateRequest request) {

        postActivityMapper.update(request.getStatus());
        bannerConfigMapper.updateBannerConfig(request);

        log.info("审核记录ID：{}", orderAuditRecord.getId());
        if (orderAuditRecord.getId() == null) {
            orderAuditRecordMapper.insertSelective(orderAuditRecord);
        } else {
            orderAuditRecordMapper.updateByPrimaryKeySelective(orderAuditRecord);
        }
    }
}
```

### 唯一约束
确保列 a 和列 b 的组合值在表中是唯一的:
UNIQUE KEY uniq_ab (a,b)
``` java
try {
} catch (DuplicateKeyException e) {
    // 添加重复异常捕获
    return R.fail("名称重复");
} catch (Exception e) {
    log.info("添加异常", e);
    return R.fail("添加失败");
}
```

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

log.info("后台标签导入任务开始执行...");
Thread.sleep(5000);
```

## http请求
### RestTemplate
公共API接口，微服务内的应用
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
            // 同步的, 会阻塞当前的执行线程
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

getForObject方法直接返回请求响应的主体（Body），它将响应体映射到你提供的类类型上。如果你只关心响应内容而不关心其它响应元数据（如状态码和头部）

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

## 环境配置
Spring boot项目
resources目录下增加文件
- application.yml
- application-dev.yml
- application-prod.yml

```yml
# application.yml
spring:
  profiles:
    active: dev  # 默认激活的配置文件，可以在启动时覆盖


# application-dev.yml
sms:
  test: true

share:
  url: https://d.x.cn


# application-prod.yml
sms:
  test: false

share:
  url: https://prod.x.cn
```

### 使用
```java
@Controller
public class BasicController {
    @Value("${sms.test}")
    private Boolean smsStatus;
    @Value("${share.url}")
    private String aiUrl;

    // http://127.0.0.1:8080/hello?name=lisi
    @RequestMapping("/hello")
    @ResponseBody
    public String hello(@RequestParam(name = "name", defaultValue = "unknown user") String name) {
        System.out.println(smsStatus);
        System.out.println(aiUrl);
        return "Hello " + name;
    }
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

# 注解
## Spring注解
@Component，@Service，@Repository，@Controller，@Configuration等注解定义的bean
### @Configuration
标记一个类作为 Java 配置类。

#### 定义 Bean
这个配置类通常包含一个或多个 @Bean 方法，这些方法会被 Spring 容器调用，以便在应用程序上下文中注册和管理 Spring Bean。
在配置类中，可以使用 @Bean 注解来定义 Bean。每个 @Bean 方法将返回一个对象，该对象会被 Spring 容器管理。

### @Autowired
Spring 会在上下文中自动查找匹配的依赖对象，并将其注入到被标注的字段、构造方法或者方法参数中。
不推荐：https://stackoverflow.com/questions/39890849/what-exactly-is-field-injection-and-how-to-avoid-it
推荐：构造器注入（它强制依赖在对象创建时就必须提供，使得类的依赖关系更加明显，也更容易实现不可变性和进行单元测试。）

### @ConfigurationProperties(prefix = "abc")
属性类用于绑定配置信息：
```java
@Data
public class AbcProperties {
    // 规则文件和决策表的路径(多个目录使用逗号分割)
    private AC a;
    @Data
    public static class AC {
        private String b;
    }
}
```

### @EnableConfigurationProperties
使使用 @ConfigurationProperties 注解的类生效。
如果一个配置类只配置@ConfigurationProperties注解，而没有使用@Component，那么在IOC容器中是获取不到properties 配置文件转化的bean。

### @RestController
一个类级别的注解，用于标记一个控制器类，表明这个类是用于处理 HTTP 请求的。@RestController 是 @Controller 和 @ResponseBody 两个注解的合成注解。
这个类中的所有方法的返回值都将自动包装JSON或XML为 HTTP 响应的正文，就无需再在每个方法上使用 @ResponseBody 注解了。
特别适合于创建 RESTful API
```java
@RestController
@RequestMapping("/users")
public class UserController {
    @GetMapping("/{id}")
    public User getUser(@PathVariable String id) {
        // 查询并返回用户，用户对象会自动转化为 JSON 格式的 HTTP 响应正文
    }
}
```

### @Controller 
注解标记的类则是传统的控制器类。它用于处理客户端发起的请求，并负责返回适当的视图（View）作为响应。在使用 @Controller 注解的类中，通常需要在方法上使用 @ResponseBody 注解来指示该方法的返回值要作为响应的主体内容，而不是解析为视图。


### @RestControllerAdvice
是一个用于整个应用程序控制器层的全局配置类
组合注解，由@ControllerAdvice、@ResponseBody组成，而@ControllerAdvice继承了@Component，因此@RestControllerAdvice本质上是个Component，用于定义@ExceptionHandler，@InitBinder和@ModelAttribute方法，适用于所有使用@RequestMapping方法。

### @Order
@Order(Ordered.HIGHEST_PRECEDENCE)
定义了组件的加载顺序，Ordered.HIGHEST_PRECEDENCE 是 Spring Framework 提供的一个常量，表示最高优先级。

### @ExceptionHandler
@ExceptionHandler({MethodArgumentNotValidException.class})
Spring 框架的一部分，它处理了MethodArgumentNotValidException，这个异常通常在使用了 @Valid 或 @Validated 的对象参数验证失败时抛出。

### ResponseStatus
@ResponseStatus(HttpStatus.OK)
设置 HTTP 响应的状态码的。这里设置为 HttpStatus.OK表示响应的 HTTP 状态是 200，也就是请求已成功。

### @ResponseBody
@ResponseBody注解表示该方法的返回结果直接写入 HTTP 响应体中，而不是通过视图解析器处理。

### @RefreshScope
Spring Cloud 中的一个注解，用于标记一个 Spring Bean，使其能够在运行时动态刷新配置。

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

### @EqualsAndHashCode(callSuper = true)
System.out.println(cat1.equals(cat2));//当callSuper属性为true时，返回false，反之则返回false

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

## @MapperScan
import tk.mybatis.spring.annotation.MapperScan;
@MapperScan 是一个 MyBatis 提供的注解，它用于指定要扫描的 Mapper 接口所在的包，以便 Spring 容器在启动时自动检测并注册这些 Mapper 接口为 Spring 管理的 Bean，无需手动为每个 Mapper 接口添加 @Mapper 注解。
例如，当你在Spring Boot应用的配置类上使用 @MapperScan(basePackages = "cn.eth.lxjkapi.mapper") 注解时，MyBatis 将会自动扫描 cn.eth.lxjkapi.mapper 包及其子包下的所有接口。对于这些接口，如果它们被识别为 Mapper 接口（通常是因为它们继承了一个或多个标记了 MyBatis 的 @Mapper 注解的父接口），MyBatis 将会自动将这些接口注册为 Bean，让你能够在 Spring 应用中自动注入和使用这些 Mapper。

## swagger注释
```java
@Api(tags = "项目") // 必填tags
@ApiOperation(value = "项目列表") // 选填valus

@Data
@ApiModel("详情入参")
public class Request {
    @ApiModelProperty(value = "ID", , required = true)
    @NotNull(message = "id不能为空")
    private Long id;
}
@ApiModel("详情")
public class Response {
    @ApiModelProperty("返回的id")
    private Long id;
}
```

## javax.validation
### @Validated
可以作用在类上
对@Valid 的封装
可以进行分组验证
```java
//分组接口 1
public interface InsertGroup {
}
//分组接口 2
public class UpdateGroup {
}

@Data
@NoArgsConstructor
public class TestRequest {
    @Null(message = "无需传id",groups = InsertGroup.class)
    @NotBlank(message = "必须传入id",groups = UpdateGroup.class)
    private String id;   
}
```

### @Valid
方法、属性（包括枚举中的常量）、构造函数、方法的形参上。
用在对象前，触发对象内部各个字段的验证。支持嵌套验证。
嵌套对象 和 集合对象，需要添加注解
```java
public R<Response> detail(@Valid @RequestBody Request request) 

@Data
public class UserBean {
    @NotNull
    private AddressBean address;

    @ApiModelProperty("标签")
    @Valid
    @Size(min = 1, max = 4, message = "标签数量异常")
    private List<ProjectTag> Tags;
}


```

### 字段校验
``` java
    @ApiModelProperty("惠票内容信息")
    @NotNull(message = "惠票内容不能为空")
    @Valid // 嵌套字段上使用 @Valid 注解
    private CouponTicketCreateRequest ticketInfo;

    @ApiModelProperty("手机号")
    @NotBlank(message = "请填写手机号")
    private String mobile;

    @NotNull(message = "优惠值不能为空")
    @Positive(message = "优惠值必须为正数")
    @ApiModelProperty("优惠值")
    @Range(min = 1, max = 999999999, message = "优惠值必须介于{min}-{max}之间")
    private Integer discount;

    @ApiModelProperty("商品标签类型：1-类目标签，2-科室标签，3-功能标签，4-数据标签")
    @NotNull(message = "类型不能为空")
    @Range(min = 1, max = 4, message = "类型不合法")
```
#### 字符
@NotNull 是一个常用的字段验证注解，用于确认字段不应为 null。可以判断空字符串
@NotEmpty: 这个注解用于集合、数组、Map、以及字符串类型的字段，确保被注解的字段不为 null 且不为空（对于字符串，长度必须大于0）。
@NotBlank: 这个注解专用于 String 类型，确保被注解的字段不为 null，除此之外还要至少包含一个非空白字符。

# MyBatis
## mapper
### updateByPrimaryKeySelective
Mapper接口中的一个方法，通常用于更新数据库表中的记录。
会基于主键更新那些非null的字段。这意味着，只有在传入的对象中非null的属性才会被更新到数据库中对应主键的记录里，其他的字段则保持原值不变。这样做的好处是可以避免覆盖那些我们不想改变的、或者我们没有提供新值的字段。
```java
int updateByPrimaryKeySelective(实体类名称 record);
```

### selectByPrimaryKey
Mapper.selectByPrimaryKey(request.getId());

### 批量更新判断记录条数
```java
int affectedRows = myMapper.batchUpdateAuditPassByIds(ids);
if (affectedRows == ids.size()) {
    System.out.println("Batch update successful. All records updated.");
}
UPDATE your_table
    SET audit_status = 'PASS'
    WHERE id IN
```

### MapKey
```java
@MapKey("ItemId")
Map<Long, Item> selectMapByItem(String no);
```

## sql
### 排序
```xml
<select id="bgList" resultType="test">
    SELECT * FROM test
    ORDER BY
    <choose>
        <when test="request.sortType == 1">
            o.id DESC
        </when>
        <when test="request.sortType == 2">
            o.id ASC
        </when>
        <otherwise>
            o.id DESC
        </otherwise>
    </choose>
</select>
```

### 时间区间
```xml
<if test="request.startTime != null and request.startTime != ''">
    and o.add_time > #{request.startTime}
</if>
<if test="request.endTime != null and request.endTime != ''">
    and #{request.endTime} > o.add_time
</if>
```

### 多条件查询
```xml
<if test="(a != null and a != '') or (b != null and b != '') or (c != null and c != '')">
    AND o.id IN (
        SELECT DISTINCT o2.id
        FROM order_info o2
        <where>
            <if test="(request.a != null and request.a != '')">
                AND t.name LIKE concat('%', #{request.a}, '%')
            </if>
        </where>
    )
</if>
```

# Example
## entity
```
这段 Java 代码定义了一个名为 `GoodsTag` 的类，该类使用了一些注解来指定其在持久化上下文中的行为。让我们逐行解释这段代码：

javax.persistence  Java Persistence API (JPA) 的核心包，扩展包

@Table(name = "goods_tag")
@Data
public class GoodsTag implements Serializable {
    @Id // 主键（Primary Key）: 使用 @Id 注解标记实体类的主键字段。
    @GeneratedValue(strategy = GenerationType.IDENTITY) //生成策略（Generation Strategies）: 使用 @GeneratedValue 注解定义主键的生成策略。
    private Long id;
}

### 逐行解释

1. **`@Table(name = "goods_tag")`**:
   - 这是一个 JPA 注解，来自 `javax.persistence` 包。
   - 它用于指定实体类对应的数据库表名。
   - 在这个例子中，`GoodsTag` 类对应的数据库表名是 `goods_tag`。

2. **`@Data`**:
   - 这是一个 Lombok 注解，来自 `lombok` 包。
   - Lombok 是一个 Java 库，可以通过注解自动生成常见的样板代码（如 getter、setter、toString、equals、hashCode 方法等）。
   - `@Data` 注解是一个综合注解，相当于同时使用了 `@Getter`, `@Setter`, `@ToString`, `@EqualsAndHashCode`, 和 `@RequiredArgsConstructor` 注解。
   - 使用这个注解，可以减少大量的样板代码，提高开发效率。

3. **`public class GoodsTag implements Serializable {}`**:
   - 这是一个普通的 Java 类声明。
   - `GoodsTag` 是类的名称。
   - `implements Serializable` 表示这个类实现了 `Serializable` 接口。
   - `Serializable` 接口是 Java 标准库中的一个接口，用于指示一个类的对象可以被序列化（即转换为字节流，以便保存到文件或通过网络传输）。
   - 实现 `Serializable` 接口通常是为了支持对象的持久化或远程传输。

### 总结

这段代码定义了一个名为 `GoodsTag` 的实体类，该类：

- 对应数据库中的 `goods_tag` 表（通过 `@Table` 注解）。
- 自动生成了 getter、setter、toString、equals、hashCode 等方法（通过 `@Data` 注解）。
- 实现了 `Serializable` 接口，使其对象可以被序列化。

这是一个典型的 JPA 实体类定义，结合了 Lombok 库来减少样板代码，从而提高开发效率和代码可读性。
```

## mapper
```java
import org.apache.ibatis.annotations.Mapper;

@Mapper
public interface GoodsTagMapper extends MyMapper<GoodsTag> {}

// mapper 自带方法
Mapper.insertSelective(record) // 只会插入非空字段
// 必需设置主键
public class CompanyInviter implements Serializable {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
record.getId(); // 是否封装了

Mapper.insertList // 会插入null

Mapper.insertUseGeneratedKeys(record)
Long generatedId = fileProcessRecord.getId();

Record record = Mapper.selectOne(new Record() {{
    setPhone(request.getPhone());
}});
```

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

```xml
<!-- status 等于 0 情况 -->
<if test="request.status != null and request.status != '' or request.status == 0">
    and status = #{request.status}
</if>
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

// 分页插件
import com.github.pagehelper.Page;
import com.github.pagehelper.PageHelper;
Page<Object> page = PageHelper.startPage(request.getPage(), request.getPageSize());
return new BasePageResponse<>((int)page.getTotal(), ret);
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

## Request
```java
@Data
@ApiModel("商品品牌厂家创建")
public class GoodsBrandCompanyCreateRequest {

    @ApiModelProperty("品牌厂家名称")
    @NotBlank(message = "品牌厂家不能为空")
    @Length(max = 50, message = "品牌厂家名称不能超过{max}字符")
    private String name;
}
```

## 全局拦截器
```java
@Configuration
public class WebConfiguretion implements WebMvcConfigurer {

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(authInteceptor()).addPathPatterns("/api/**");
    }

    @Bean
    public AuthInteceptor authInteceptor() {
        return new AuthInteceptor();
    }
}
```

# 消息队列
消息队列（Message Queue，简称MQ）是用于在分布式系统中实现异步通信的一种机制。它允许不同的系统或服务之间通过消息进行通信，而不需要直接调用彼此的API。这种机制可以帮助解耦系统，提高系统的可扩展性和可靠性。

# Utils
## uuid
UUID.randomUUID()

## ulid
```java
<dependency>
  <groupId>com.github.f4b6a3</groupId>
  <artifactId>ulid-creator</artifactId>
  <version>5.2.3</version>
</dependency>

Ulid ulid = UlidCreator.getMonotonicUlid();
```

## Time
当前时间
```java
Date now = new Date();
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM");
String formattedDate = sdf.format(now);

import org.apache.commons.lang3.time.DateFormatUtils;
String currentTime = DateFormatUtils.format(new Date(), "yyyy-MM-dd");
```

### 其他时间
```java
import org.apache.commons.lang3.time.DateFormatUtils;
// 预计发货时间
if (ret.getShippingTime() == null) {
    // orderItems中每项有 sendOutType，0:当日，1:24小时，2:48小时。找出最小的一项
    int sendOutType = items.stream().map(OrderInfoItemBgDetailResponse::getSendOutType).min(Integer::compareTo).orElse(0);
    // 当sendOutType为0时，当天的23:59:59。等于1或2加对应天数
    Calendar calendar = Calendar.getInstance();
    calendar.setTime(ret.getAddTime());
    if (sendOutType == 0) {
        calendar.set(Calendar.HOUR_OF_DAY, 23);
        calendar.set(Calendar.MINUTE, 59);
        calendar.set(Calendar.SECOND, 59);
        calendar.set(Calendar.MILLISECOND, 999);
    } else {
        calendar.add(Calendar.DAY_OF_MONTH, sendOutType);
    }
    ret.setPredictShippingTime(DateFormatUtils.format(calendar.getTime(), "yyyy-MM-dd HH:mm:ss"));
}
```

## equals
```java
// 两个null为true，字符串/数字都正常
import java.util.Objects;
if(!Objects.equals(request.getCode(), redisCode)){
    return R.fail("验证码错误");
}
```

## 批量处理
```java
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9);
int batchSize = 3;
int totalSize = list.size();
int batchCount = (totalSize + batchSize - 1) / batchSize;
System.out.println(batchCount);
for (int i = 0; i < batchCount; i++) {
    int start = i * batchSize;
    int end = Math.min(start + batchSize, totalSize);
    List<Integer> subList = list.subList(start, end);
    System.out.println(subList);
}
```

## 逗号处理
```java
// 逗号拼接
String notSupportProvinceIds = notSupportList.stream().map(ExpressAreaConfig::getProvinceId).map(Objects::toString).collect(Collectors.joining(","));
// 逗号转数组
List<Long> provinceIds = Arrays.stream(area.getProvinceIds().split(",")).map(o->Long.valueOf(o)).collect(Collectors.toList());

// 分号拼接
List<String> names = new ArrayList<>();
String.join("；", names)
```

## 排除
```java
List<String> failExpressNos = new ArrayList<>();
Set<String> failExpressNoSet = new HashSet<>(failExpressNos);
// 创建一个新的列表来存储成功的快递单号
List<String> successExpressNos = new ArrayList<>();
// 遍历 expressNoList，将不在 failExpressNoSet 中的元素添加到 successExpressNos 中
for (ExpressInfoRequest expressInfo : request.getExpressList()) {
    if (!failExpressNoSet.contains(expressInfo.getExpressNo())) {
        successExpressNos.add(expressInfo.getExpressNo());
    }
}
```

## 分批插入
```java
public void batchInsertAdGroupWhitelist(Long adGroupId, List<String> nos) {
    // 根据ethNos的长度，进行每5000个一次的批量插入
    int batchSize = 5000;
    int totalSize = nos.size();
    int batchCount = (totalSize + batchSize - 1) / batchSize;
    log.info("AdBiz 广告群组白名单批量插入, 总条数: {}, 每批次条数: {}, 批次数: {}", totalSize, batchSize, batchCount);

    for (int i = 0; i < batchCount; i++) {
        int start = i * batchSize;
        int end = Math.min(start + batchSize, totalSize);
        List<String> batchList = nos.subList(start, end);
        adGroupWhitelistMapper.batchInsert(adGroupId, batchList);
    }
}
```

## 分批处理
```java
Long maxId = logisticsPushRespMapper.selectMaxId();
if (null == maxId) {
    maxId = 0L;
}
Long minId = 0L;

int size = 300;

List<LogisticsPushResp> list = logisticsPushRespMapper.selectByRange(minId, maxId, size);
while (!CollectionUtils.isEmpty(list)) {
    for (LogisticsPushResp push : list) {
        minId = push.getId();
        // 业务处理
    }
    list = logisticsPushRespMapper.selectByRange(minId, maxId, size);
}

// 分批查询待收货状态：PENDING_RECEIPT 的订单
Long maxId = orderInfoMapper.selectPendingReceiptMaxId();
log.info("待收货订单最大ID: {}", maxId);
if (maxId == null) {
    return;
}
Long minId = orderInfoMapper.selectPendingReceiptMinId();
log.info("待收货订单最小ID: {}", minId);
if (minId == null) {
    return;
}
Integer batchSize = 300;
while (minId <= maxId) {
    List<OrderInfo> orderInfoList = orderInfoMapper.batchSelectPendingReceiptRange(minId, maxId, batchSize);
    log.info("分批查询待收货订单数量: {}", orderInfoList.size());
    if (CollectionUtils.isEmpty(orderInfoList)) {
        break;
    }
    // 业务处理
    minId = orderInfoList.get(orderInfoList.size() - 1).getId() + 1;
    log.info("下一轮循环的最小ID: {}", minId);
}
```

## 数据按部分字段合并
```java
// 过滤出 support_type = 1的所有记录
List<ExpressAreaConfig> supportList = areaConfigList.stream().filter(item -> item.getSupportType().equals(ExpressAreaConfig.SupportTypeEnum.送达.code)).collect(Collectors.toList());

Map<ExpressAreaConfigPrice, List<ExpressAreaConfig>> groupedSupportList = new HashMap<>();
for (ExpressAreaConfig record: supportList) {
    ExpressAreaConfigPrice key = new ExpressAreaConfigPrice(record.getInitKg(), record.getInitPrice(), record.getAddKg(), record.getAddPrice());
    groupedSupportList.computeIfAbsent(key, k -> new ArrayList<>()).add(record);
}
// 将分组后的记录转换为列表
List<List<ExpressAreaConfig>> result = new ArrayList<>(groupedSupportList.values());
for (List<ExpressAreaConfig> group : result) {
    String supportProvinceIds = group.stream().map(ExpressAreaConfig::getProvinceId).map(Objects::toString).collect(Collectors.joining(","));
    ExpressAreaConfigListResponse areaConfigResponse = new ExpressAreaConfigListResponse();
    areaConfigResponse.setProvinceIds(supportProvinceIds);
    areaConfigResponse.setSupportType(ExpressAreaConfig.SupportTypeEnum.送达.code);
    areaConfigResponse.setInitKg(group.get(0).getInitKg());
    areaConfigListResponses.add(areaConfigResponse);
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

## 新建创建 Spring Initializr项目
[阿里云原生应用脚手架](https://start.aliyun.com/)
创建Spring boot项目
JDK 1.8 就是 Java 8
Java最低只能选17问题
修改Server URL 为：https://start.aliyun.com/

### 选择依赖
Spring Web：用于构建 Web 应用程序。
Spring Data JPA：用于数据访问。
Spring Boot DevTools：用于开发时的热部署。
Thymeleaf：用于模板引擎。
Spring Security：用于安全性。
MySQL Driver：用于 MySQL 数据库连接。

### 访问应用程序
启动 Application.java 文件
http://localhost:8080

## 安装插件
默认无法访问安装
Settings -> HTTP Proxy Settings -> Auto-detect proxy settings -> 配置网址：https://plugins.jetbrains.com/idea


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

## Failed to configure a DataSource: 'url' attribute is not specified and no embedded
排除DataSourceAutoConfiguration的自动配置
```java
@SpringBootApplication(exclude= {DataSourceAutoConfiguration.class})
//@SpringBootApplication
public class SpringenvApplication {
    public static void main(String[] args) {
        SpringApplication.run(SpringenvApplication.class, args);
    }
}
```

## no main manifest attribute, in /app.jar 
https://stackoverflow.com/questions/9689793/cant-execute-jar-file-no-main-manifest-attribute
## docker启动报错： Exception in thread "main" java.lang.NoClassDefFoundError: org/springframework/boot/SpringApplication
Maven 配置中可以看出，你已经配置了 spring-boot-maven-plugin，但你设置了 <skip>true</skip>，这会跳过 Spring Boot 插件的执行，导致生成的 JAR 文件中没有包含 Spring Boot 的依赖项。

``` xml
<build>
    <finalName>app</finalName>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
                <encoding>UTF-8</encoding>
            </configuration>
        </plugin>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-jar-plugin</artifactId>
            <version>3.0.2</version>
            <configuration>
                <archive>
                    <manifest>
                        <addClasspath>true</addClasspath>
                        <classpathPrefix>lib/</classpathPrefix>
                        <mainClass>com.example.springenv.SpringenvApplication</mainClass>
                    </manifest>
                </archive>
            </configuration>
        </plugin>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <version>${spring-boot.version}</version>
            <executions>
                <execution>
                    <goals>
                        <goal>repackage</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>

```

## 没有主清单属性
$ java -jar hellospring-0.0.1-SNAPSHOT.jar 
hellospring-0.0.1-SNAPSHOT.jar中没有主清单属性
``` xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <version>${spring-boot.version}</version>
            <executions>
                <execution>
                    <goals>
                        <goal>repackage</goal>
                    </goals>
                </execution>
            </executions>
         </plugin>
    </plugins>
</build>
```

## No serializer
Servlet.service() for servlet [dispatcherServlet] in context with path [] threw exception [Request processing failed; nested exception is org.springframework.http.converter.HttpMessageConversionException: Type definition error: [simple type, class com.kaifaweb.hellojdbc.demos.entity.Test]; nested exception is com.fasterxml.jackson.databind.exc.InvalidDefinitionException: No serializer found for class com.kaifaweb.hellojdbc.demos.entity.Test and no properties discovered to create BeanSerializer (to avoid exception, disable SerializationFeature.FAIL_ON_EMPTY_BEANS) (through reference chain: java.util.ArrayList[0])] with root cause

``` java
@Data
public class Test implements Serializable {}
```

## IDEA提示 It's possible to extract method returning 'orderAuditRecords' from a long surrounding method。
代码如下：orderAuditRecord.setRefusalReason("");
可以从一个较长的方法中提取一个返回 orderAuditRecords 的方法。这通常是为了提高代码的可读性和可维护性。