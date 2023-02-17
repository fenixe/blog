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

## 数据放在内存中
数据库对应地址修改，要重新跑一下项目


## 工具类/方法
### StringUtils
isNotBlank 
StringUtils.isNotBlank(" ") = false

isNotEmpty
StringUtils.isNotEmpty(" ") = true

### BeanConvertUtils
BeanConvertUtils.trimBean(request);
request.name = " ki l " => request.name = "kil"

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
