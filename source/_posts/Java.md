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
            // 基本判断：非空
            return adminService.createAdmin(request);
        } catch(Exception e){
            log.error("{}", e);
            return R.fail(GlobalRetCode.服务器内部错误.code, GlobalRetCode.服务器内部错误.name(), null);
        }
     }
}
```
