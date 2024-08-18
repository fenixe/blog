---
title: Spring
date: 2024-08-14 21:51:44
categories:
- Java
tags:
- Spring
---

# Base
用于构建企业级应用的轻量级一站式解决方案
核心代码：IOC、AOP

## Spring家族成员
1. Spring Framework
2. Spring Boot
3. Spring Cloud

https://spring.io/projects

## 异步
WebFlux

# Spring Boot
用最少的时间和精力构建一个基于Spring的应用程序

## Spring Boot Actuator
监控和管理 Spring Boot 应用程序的生产就绪功能
常用的 Actuator 端点：
/actuator/health：显示应用程序的健康信息。
curl http://localhost:8080/actuator/health

## JDBC
Spring Boot 1.0 中使用：
tomcat 的 data source

Spring Boot 2.0 中默认使用：
HikariCP（光·快）

Druid 阿里巴巴开源数据库连接池项目。监控强大。

### 事务
- Spring 的声明式事务本质上是通过AOP来增强了类的功能
- Spring 的AOP本质上就是为了类做了一个代理
    看似在调用自己写的类，实际用的是增强后的代理类
``` java
@Service
public class UserBiz {
    // 生效
    @Transactional(rollbackFor = {Exception.class, RuntimeException.class})
    public void insertThenRollback() throws Exception {
        User user = new User();
        user.setName("Hi3");
        userMapper.insert(user);
        throw new RuntimeException();
    }

    // 无效
    // 没有事务代理
    public void invokeInsertThenRollback() throws Exception {
        insertThenRollback();
    }
}
```

## 注解
### Java Config相关注解
- @Configuration
    标注当前类是配置类

- @ImportResource
    注入配置以外的，xml配置文件

- @ComponentScan
    告诉Sping容器，可以扫描那些package下的Bean配置

- @Bean
    在Java Configuration的类中，如果方法被标注，它的返回就可以作为Spring Bean的配置存在于整个Spring Bean的 contexts中

- @ConfigurationProperties
    注入配置，方便使用

### 常用的 Bean 注解
通过注解定义 Bean
- @Component
    通用的注解定义一个通用的Bean。所有的Java Bean都可以使用@Component来定义。下面的注解都是语意注解
- @Repository
    数据操作的仓库，数据库的访问层
- @Service
    业务的服务层
- @Controller
    Spring MVC。Web层的Bean
  - @RestController
      Rest Web Server
- @RequestMapping
    类下面的 方法是在那些url下的映射

与Bean注入相关的注解
- @Autowired
    上下文中按照类型做查找注入进来
- @Qualifier
    多个同类型的，@Autowired有歧义，容器会找错，指定Bean的名字
- @Resource
    根据名字注入
- @Value
    注入常量，@Value(${}) spel表达式，找到上下文配置的一些东西

### 数据操作用的mybatis。在写mapper接口时，应该使用@Repository 还是 @Mapper 注解
在使用 MyBatis 时，推荐使用 @Mapper 注解来标记你的 Mapper 接口。这是因为 @Mapper 注解是 MyBatis 提供的专门用于标记 Mapper 接口的注解，它能够让 MyBatis 自动扫描并识别这些接口，从而生成相应的实现类。

@Repository 注解是 Spring 提供的，用于标记数据访问层的组件。虽然你可以在 MyBatis 的 Mapper 接口上使用 @Repository 注解，但这不是最佳实践，因为它并不能让 MyBatis 自动识别和扫描这些接口。

# Spring Cloud
高可用的应用程序
简化了分布式系统的开发
从单机向集群向云发展的过程，更快、更好、更轻松的去开发一套基于云的应用程序
- 配置管理
- 服务注册与发现
- 熔断
- 服务追踪
