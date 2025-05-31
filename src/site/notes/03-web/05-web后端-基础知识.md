---
{"dg-publish":true,"permalink":"/03-web/05-web后端-基础知识/","dgPassFrontmatter":true}
---


#已实践

## 1. Tomcat

动态资源，静态资源。

### 1.1. 介绍和使用

apache开源免费的 web 轻量级服务器（web 容器 | servlet 容器）

文件夹
- bin
- conf
- webapps

需要正确配置 `JAVA_HOME` 环境变量。

### 1.2. 配置

- 启动日志窗口乱码，配置文件改编码 `GBK`
- `BindException`
	- `server. xml` 配置改端口。
	- 查看端口占用情况，杀死对用的进程

windows
```cmd
#cmd 打开 resmon 资源监视器

```

linux
```bash
netstat -ano | findstr 8080
根据进程pid结束进程

kill -9 pid 杀死进程
```

## 2. Servlet

### 2.1. 介绍-入门程序

- Servlet 是 Java 程序，运行在 tomcat 中。
- 通过 http 协议，接收请求，然后响应客户端数据。
- JavaEE 规范（接口）之一

maven 项目（pom 打包方式默认是 jar），pom 设置 war .

依赖
javax.servlet-api 作用范围是 main 和 test 文件夹，不参与打包。`provided`

实现接口，或继承类，重写 doGet 方法。
```java
resp.setContentType("text/html;charset=utf-8");
resp.getWritter().write(msg);

@WebServlet(urlPatterns="/hello")
req.getParameter("name")
```

### 2.2. 配置 Tomcat

IDEA 配置
- 添加一个 Tomcat。
- 添加应用，war 包，设置项目路径。

### 2.3. 执行流程

tomcat 根据路径找 servlet，然后调用 servelt 的方法。

## 3. Http 协议

- http 协议是一个浏览器和服务器之间传输数据的规则。
- 基于 tcp
- 一次请求对应一个响应。
- 无状态，速度快。

### 3.1. 请求数据格式

```
请求行（请求类型 路径 协议/版本）
请求头（key:value）
空行
请求体
```

### 3.2. 请求信息获取

```java
// HttpServletRequest 方法

getMethod()
getRequestURI()
getRequestURL()
getScheme()
getHeader()
getParameter()
getQueryString()

//maven插件版本修改 maven-war-plugin改 3.4.0
```

### 3.3. 响应数据格式

```
响应行（协议/版本 状态码 描述）
响应头（key:value） value值application/json
Cache-Control:
响应体
```

状态码：
- 1 xx
- 2 xx
- 3 xx
- 4 xx `HttpStatus.SC_UNAUTHORIZED` 401
- 5 xx

### 响应数据设置

```java
HttpServletResponse
setStatus()
setHeader()
```


> [!important]+ 
> 
> 编码问题？ #TODO
> 


## 4. SpringBoot-Web 入门
### 4.1. 介绍

spring. io spring 生态。

springboot 编程快，简单，安全。

- 都依赖 spring framework
- 4.0 后，出现了 SpringBoot（简化配置，快速开发）

### 4.2. 快速入门

- 创建项目（spring 初始化器）
- 设置包名、group
- pom 加依赖（注意 spring web boot 的版本）

```java
@RestController
@RequestMapping
```

页面的 JDK 选择下拉框，有对版本限制。

### 4.3. 快速入门方式二

创建 maven 的一套。
pom 加 parent, spring-boot-starter-web
添加启动方法。

### 4.4. 修改端口

application.properties/yml 改端口

### 4.5. 入门程序解析

- Springboot 起步依赖，内置 Tomcat
- DisPatcherServlet (看源码，右键 diagram), 前端控制器，把请求转发到相应的 Controller 里

doDispatch 方法

### 4.6. 打包和安装

**maven 插件** spring-boot-maven-plugin 打包插件。

- `package` 打包
- `install` 安装到本地仓库
- `deploy` 发布到私服




[[03-web/04-web后端-maven基础\|上一节：04-web后端-maven基础]]

[[03-web/06-web实战-ioc-di\|下一节：06-web实战-ioc-di]]
