---
{"dg-publish":true,"permalink":"/03-web/09-web实战-部门管理/","dgPassFrontmatter":true}
---


## 1. 接口开发

- 请求方式
- 请求路径
- 请求参数
- 响应结果

## 2. 请求参数

请求路径是 Controller 上的和方法上的拼接

### 2.1. 路径上的参数，接受参数
- 原始的方式
- 注解@RequestParam
- 省略注解@RequestParam
- @PathVariable

### 2.2. 请求体里的参数
@RequestBody

请求体里的参数json，RequestBody参数用它标注实体接受。


## 3. 新增注意事项

新增的时候，填充默认值


## 4. sql 中占位符注意事项
- `#{} ` 会生成**预编译 sql**，位置替换成? 把参数当成一个整体传入。
- `${}` sql 会**字符串拼接**

## 5. 动态 sql 
更新的时候，动态 sql
- , 确保 null 参数，不更新。

## 6. 删除



## 7. 新增


## 8. 修改部门

- 回显
- 修改

## 9. 日志技术-logback

- springboot 项目不用引用 logback 的依赖，因为springboot 的依赖里包含了它。
- logback. xml 需要值的东西
	- log-level


> [!cite]+ 
> 
> https://logback.qos.ch/ 
 

![assets/03-web/09-web实战-部门管理/IMG-20250530-170350-961.png](/img/user/assets/03-web/09-web%E5%AE%9E%E6%88%98-%E9%83%A8%E9%97%A8%E7%AE%A1%E7%90%86/IMG-20250530-170350-961.png)

使用 demo

logback. xml
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<configuration>  
    <!-- 控制台输出 -->  
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">  
       <encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">  
          <!--格式化输出：%d 表示日期，%thread 表示线程名，%-5level表示级别从左显示5个字符宽度，%msg表示日志消息，%n表示换行符 -->  
          <pattern>%d{HH:mm:ss} [%thread] %-5level %logger{50}  -  %msg%n</pattern>  
       </encoder>    </appender>  
    <!-- 按照每天生成日志文件 -->  
    <appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">  
       <rollingPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedRollingPolicy">  
          <!-- 日志文件输出的文件名, %i表示序号 -->  
          <FileNamePattern>D:/tlias-%d{yyyy-MM-dd}-%i.log</FileNamePattern>  
          <!-- 最多保留的历史日志文件数量 -->  
          <MaxHistory>30</MaxHistory>  
          <!-- 最大文件大小，超过这个大小会触发滚动到新文件，默认为 10MB -->          <maxFileSize>10MB</maxFileSize>  
       </rollingPolicy>  
       <encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">  
          <!--格式化输出：%d 表示日期，%thread 表示线程名，%-5level表示级别从左显示5个字符宽度，%msg表示日志消息，%n表示换行符 -->  
          <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{50}-%msg%n</pattern>  
       </encoder>    </appender>  
    <!-- 日志输出级别 trace < debug < info < warn < error -->    <root level="info">  
       <appender-ref ref="STDOUT" />  
       <appender-ref ref="FILE" />  
    </root></configuration>
```

[[03-web/08-web实战-java操作数据库\|上一节：08-web实战-java操作数据库]]

[[03-web/10-web实战-多表操作-员工列表查询\|下一节：10-web实战-多表操作-员工列表查询]]