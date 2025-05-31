---
{"dg-publish":true,"permalink":"/03-web/11-web实战-新增员工/","dgPassFrontmatter":true}
---


## 1. 新增员工

主表明细表

- 返回主键给实体
- 明细表动态 sql-批量插入 `foreach`

```java
 @Options(useGeneratedKeys = true, keyProperty = "id")   //获取主键的值并赋给id属性
```

```xml
<insert id="insert" useGeneratedKeys="true" keyProperty="id">
```

## 2. 事务管理

事务和传播

```java
@Transational(rollbackfor=Exception.class, Propagation=Transation.REQUIRED)

//Transation.REQUIRED
//Transation.REQUIRE_NEW

A->事务方法B
//B上注解的值：
//Transation.REQUIRED 如果A有事务，加入。没有，自己创建事务。
//Transation.REQUIRE_NEW 不管A，自己创建新的事务

yml配置

#打开spring事务管理的debug日志  
logging:  
  level:  
    org:  
      springframework:  
        jdbc:  
          support:  
            JdbcTransactionManager: debug
   
```


## 3. 上传文件

### springboot 本地上传，和注意事项

表单要求：
- 表单 `method = "post" `
- 表单 `enctype= "multipart/form-data" `
- 表单 `<input type="file">`

后端代码

```java
@PostMapping("/upload")
public Result upload(MultipartFile file) {
    String file = file.getOriginalName();
    String suffix = file.substract(file.lastIndexOf("."));
    String name = UUID.randomUuid() + suffix;
    file.transferTo(new File("D:/images/"+name));
}
```

配置

```yml
//spring:下
servlet:  
  multipart:  
    #单个文件最大可上传的大小，默认时1MB  
    max-file-size: 10MB  
    #单次请求所有文件最大可上传的大小，默认时10MB  
    max-request-size: 100MB
```


### 阿里云 OSS 

> [!cite]+ 
> 
> https://help.aliyun.com/zh/oss/developer-reference/sdk-code-samples/?spm=a2c4g.11186623.help-menu-31815.d_5_2.7a251a9cLwCiyj

准备：
- 控制台，找到 OSS，开通。
- 创建 bucket
- 头像右键-创建 access-key
- 然后看 oss 的 sdk 文档
- 测试类

注解：
```java
//获取单个属性
@Value("${oss.key}")
private String key;


@Data
@Component
@ConfigurationProperites(prefix="oss")
//配置类 获取yml得多个属性


#自定义配置  
aliyun:  
  oss:  
    endpoint: https://oss-cn-shenzhen.aliyuncs.com  
    bucket: xxxx
```


## 4. 配置文件

yml 注意事项：
- `#` 表示注解
- `key: value` 冒号后值前有个空格
- 值是数字以 0 开头表示 8 进制。
- 缩进不能用 tab（idea 中可以，转化tab 为 4 空格）

```yml
# app 表示的对象(map) key-value键值对
app:
  name: jack
  version: 1
  # users表示的 数组/集合
  users:
    - jack # 作者1
    - tom # 作者2
    - john # 作者3
```

[[03-web/10-web实战-多表操作-员工列表查询\|上一节：10-web实战-多表操作-员工列表查询]]

[[03-web/12-web实战-删除-修改\|下一节：12-web实战-删除-修改]]
