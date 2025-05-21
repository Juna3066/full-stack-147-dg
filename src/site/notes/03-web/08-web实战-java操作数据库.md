---
{"dg-publish":true,"permalink":"/03-web/08-web实战-java操作数据库/","dgPassFrontmatter":true}
---



## 1. JDBC

数据库操作技术，市场占比：
- mybatis 46%
- mybatis-plus 24%
- spring data jpa 11%


### 1.1. 概述

- **JDBC**（Java Database Connection）**是 Java 自带的 API**。
- JDBC 具体由数据库厂商实现。（联想到 Java 的 SPI 机制）
- 程序员只用学这一套 API, 就可以操作各种数据库。

Mysql 8 的驱动包是 mysql-connector-java. jar jar 包存在于运行时。（编译时不需要）

### 1.2. 快速入门

`com.mysql.cj.jdbc.mysql`

步骤：
1. **注册**驱动
2. **获取**连接
3. **获取**执行对象
4. **执行** SQL
5. **释放**资源

```java

```

### 1.3. 常见错误

异常，从上往下看，自己写一个异常，实践下。 #TODO 

## 2. JDBC 的 API 详解

### 2.1. DriverManager

DriverManager 用来注册驱动，获取数据库连接。
- `DriverManager.getConnection(url,username,password)`
- `jdbc:mysql//ip:port/dbname` 本地数据库 `ip:port可省略`，`jdbc:myslq:///dbname`

**SPI 机制**
- 是 **JDK 内置的服务提供发现机制**。
- 能轻松扩展你的程序，方便的切换实现。实现接口和类的解耦。（联想：面向接口编程，多态）
- 会加载 `META-INF` 目录下的配置文件中的类信息。 #TODO 

![assets/03-web/08-web实战-java操作数据库/IMG-20250521-165447-889.png](/img/user/assets/03-web/08-web%E5%AE%9E%E6%88%98-java%E6%93%8D%E4%BD%9C%E6%95%B0%E6%8D%AE%E5%BA%93/IMG-20250521-165447-889.png)

> [!important]+ 
> 
> 全类名、全限定名? 记个标准的叫法。


### 2.2. Connection 和 Statement

```java
executeUpdate(sql) 返回 int
executeQuery(sql) 返回 ResultSet

[Prepared]Statement [预编译]
```

### 2.3. ResultSet

```java
next()
getXxx()
getInt()
getString()
```

### 2.4. ResultSet 参数化测试

#TODO 

@CsvSource ({"x","2"})

### 2.5. PreparedStatement 和 SQL 注入

预编译 SQL，能防止 SQL 注入。
```

"select * from t_user where id = "tom" and password = "传入的字符串" ;
如果字符串是：" or "1" = "1
字符串拼接结果：
"select * from t_user where id = "tom" and password = "" or "1" = "1" ;

```



> [!important]+ 
> 
> or 和 and 在 SQL 的顺序
> 关联 SQL 查询


联想当 mybatis 面试题

```
${} 和 #{}  后者是预编译SQL；字符串拼接，占位符替换。
```

### 2.6. 预编译 SQL 的好处

安全，同时性能更好了。

- 有语法检查
- 有缓存，sql 要编译再执行，预编译能减少编译次数。

## 3. Mybatis 基础
### 3.1. 介绍

- Mybatis 是持久层框架，简化了 JDBC 的开发。
- apache 的项目。

DAO （Data Access Object）数据访问对象。

### 3.2. 快速入门 

- 依赖 `mysql和mybatis`
- application. properties 配置数据库连接池信息。
- 写 Mapper接口（代替 dao） `@Mapper` 注解接口，`@Select("sql")` 注解接口方法
- 编写 test 类，注解 `@SpringBootTest` 用 spring 环境 IOC 容器进行测试。**测试类和引导类的包，要一致。否则，需要指定启动类**，`@SpringBootTest(classes=App.class)`

IDEA 插件- `grep console`


```java


```

### 3.3. 辅助配置 
### 3.4. JDBC 对比 Mybatis
### 3.5. 数据库连接池
### 3.6. XML 映射文件
### 3.7. MybatisX 插件和映射路径的配置
### 3.8. 部门列表查询-集成 Mybatis
### 3.9. 部门列表查询-数据封装

[[03-web/07-web实战-数据库\|上一节：07-web实战-数据库]]

[[03-web/15-web实战-登录认证\|下一节：15-web实战-登录认证]]
