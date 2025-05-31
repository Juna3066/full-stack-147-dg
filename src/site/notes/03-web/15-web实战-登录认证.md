---
{"dg-publish":true,"permalink":"/03-web/15-web实战-登录认证/","dgPassFrontmatter":true}
---


## 1. 登录校验思路 ?

**登录标记**：
用户登录成功后，后续的每次请求，都可以获取到这个标记。

会话技术，维护浏览器状态的方法。

服务器需要识别多次请求是否来自同一个浏览器，便于同一次会话，的多次请求的数据共享。

会话跟踪技术：
- Cookie http 协议支持。移动端无法使用。用户可以禁用。cookie 不能**跨域**。
- Session

跨域：
- 协议
- ip/域名
- 端口

## 2. 会话跟踪技术
### 2.1. Cookie 的原理？

响应头里的
```
Set-Cookie:name=value
```

请求头里的
```
Cookie:name=value
```

```java
@GetMapping("/c1")  
public Result cookie1(HttpServletResponse response){  
	//Set-Cookie:login_username:tom
    response.addCookie(new Cookie("login_username","tom")); 
    return Result.success();  
}  
  
//获取Cookie  
@GetMapping("/c2")  
public Result cookie2(HttpServletRequest request){ 
	//Cookie:login_username:tom
    Cookie[] cookies = request.getCookies();  
    for (Cookie cookie : cookies) {  
        if(cookie.getName().equals("login_username")){  
            log.info("login_username: {}",cookie.getValue());
        }  
    }  
    return Result.success();  
}

```

### 2.2. 会话跟踪技术 Cookie 优缺点？

优点：
- http 协议支持的技术

缺点：
- 移动端 app 不能用 Cookie
- 不安全，用户可以禁用 Cookie
- Cookie 不能跨域


### 2.3. 会话跟踪技术 Session 的原理?

底层基于 Cookie
- Set-Cookie: JESSIONID=xxxxx (指的是 session.getId () HttpSession 的 id)
- Cookie: JESSIONID=xxxxx

```java
@GetMapping("/s1")  
public Result session1(HttpSession session){  
    log.info("id:{}",session.getId());  
    log.info("HttpSession-s1: {}", session.hashCode());  
    session.setAttribute("loginUser", "tom"); //往session中存储数据  
    return Result.success();  
}  
  
@GetMapping("/s2")  
public Result session2(HttpServletRequest request){  
    HttpSession session = request.getSession();  
    log.info("HttpSession-s2: {}", session.hashCode());  
  
    Object loginUser = session.getAttribute("loginUser"); //从session中获取数据  
    log.info("loginUser: {}", loginUser);  
    return Result.success(loginUser);  
}
```



### 2.4. 会话跟踪技术Session 的优缺点？

优点：
- 存在服务器端，安全。

缺点：
- 服务器集群环境下不能直接使用 Session (需要 Session 共享)
- Cookie 的缺点

## 3. 会话跟踪技术令牌 Token

### 3.1. 优缺点

优点：
- 支持 PC 和移动端 app
- 解决集群环境下的认证问题
- 减轻服务器存储压力

缺点：
- 需要自己实现
	- 登录成功后，令牌的生成。
	- 每次请求，对前端请求头携带的 token 的校验。
		- 过滤器 Filter或拦截器 Inteceptor。

```java
@Override  
public LoginInfo login(Emp emp) {  
    Emp empLogin = mapper.getUsernameAndPassword(emp);  
    if(empLogin != null){  
        //1. 生成JWT令牌  
        Map<String,Object> dataMap = new HashMap<>();  
        dataMap.put("id", empLogin.getId());  
        dataMap.put("username", empLogin.getUsername());  
  
        String jwt = JwtUtils.generateJwt(dataMap);  
        LoginInfo loginInfo = new LoginInfo(empLogin.getId(), empLogin.getUsername(), empLogin.getName(), jwt);  
        return loginInfo;  
    }  
    return null;  
}
```


![assets/03-web/15-web实战-登录认证/IMG-20250531-215144-539.png](/img/user/assets/03-web/15-web%E5%AE%9E%E6%88%98-%E7%99%BB%E5%BD%95%E8%AE%A4%E8%AF%81/IMG-20250531-215144-539.png)


### 3.2. JWT 有几个组成部分？

每个部分存的内容是什么？

- header 头。存的是，令牌类型，签名算法。
- payload 载荷。存的是，后端自定义的信息。
- signature 签名。存的是签名，保证安全性。
	- 防止 token 被篡改，
	- 指定**签名算法**，指定**密钥**
	- 把 header 和 payload 作为**参数**
	- **计算**而来

![assets/03-web/15-web实战-登录认证/IMG-20250531-220024-983.png](/img/user/assets/03-web/15-web%E5%AE%9E%E6%88%98-%E7%99%BB%E5%BD%95%E8%AE%A4%E8%AF%81/IMG-20250531-220024-983.png)


**Base 64**：

是一种基于 64 个可打印字符（A-Z a-z 0-9 + /）来表示二进制数据的编码方式。

### 3.3. 怎么生成令牌？

```xml
jjwt
0.9.1
```

```java
map.put("id",101);
map.put("username","tom")
String jwt = Jwts.builder()
  .signWith(SignatureAlgorithm.HS256, "xxx")
  .addClaims(map)
  .setExpiration(new Date(System.currentTimeMillis() + EXPIRATION_TIME_MS))
```

### 3.4. JWT 的生成和校验？

- `Jwts.builder().`
- `Jwts.parser(). `

### 3.5. 解析令牌什么情况报错？

- 被篡改
- 过期失效

```java
@Test  
public void test() {  
    Map<String, Object> claims = new HashMap<>();  
    claims.put("id", 10);  
    claims.put("username", "tom");  
    String jwt = Jwts.builder().signWith(SignatureAlgorithm.HS256, "666888").addClaims(claims)  
            //.setExpiration(new Date(System.currentTimeMillis() +  100))  
            .setExpiration(new Date(System.currentTimeMillis() + 60 * 60 * 1000)).compact();  
    System.out.println(jwt);  
    //io.jsonwebtoken.ExpiredJwtException:  
    Claims claims2 = Jwts.parser().setSigningKey("666888").parseClaimsJws(jwt).getBody();  
    System.out.println(claims2);  
    //io.jsonwebtoken.MalformedJwtException  
    String s = jwt.replaceAll("\\d", "0");  
    System.out.println("s = " + s);  
    Claims claims3 = Jwts.parser().setSigningKey("666888").parseClaimsJws(s).getBody();  
    System.out.println(claims3);  
}
```

## 4. 过滤器

### 4.1. Filter 的开发步骤？

- 定义类实现 Filter 接口
	- init 方法实现
		- 初始化方法, web服务器启动, 创建Filter实例时调用, 只调用一次
	- doFilter 方法实现
		- 拦截到请求时,调用该方法,可以调用多次
	- destory 方法实现
		- 销毁方法, web服务器关闭时调用, 只调用一次
- 配置
	- `@WedFilter(urlPattern="/*")`
	- `@ServletComponentScan` 开启 Servlet 组件扫描


> [!important]+ 
> 过滤器放行：chian. doFilter (req, resp);
> 
> 过滤器如果不执行放行操作，
> 
> 过滤器拦截到请求后，就不后访问到对应的资源。



### 4.2. 过滤器执行流程？

- 放行前
- 放行
- 资源
- 放行后

### 过滤器链 

注意过滤器链
- 多个过滤器组成的一条链路。
- 执行优先级是按时过滤器类名的自动排序确定的，类名排名越靠前，优先级越高

![assets/03-web/15-web实战-登录认证/IMG-20250531-222216-607.png](/img/user/assets/03-web/15-web%E5%AE%9E%E6%88%98-%E7%99%BB%E5%BD%95%E8%AE%A4%E8%AF%81/IMG-20250531-222216-607.png)

![assets/03-web/15-web实战-登录认证/IMG-20250531-232945-249.png](/img/user/assets/03-web/15-web%E5%AE%9E%E6%88%98-%E7%99%BB%E5%BD%95%E8%AE%A4%E8%AF%81/IMG-20250531-232945-249.png)

### 4.3. 过滤器拦截路径例子？

- `/login` 拦截具体路径
- `/*` 所有资源的访问，都拦截
- `/emps/*` **拦截目录**/emps 下的所有资源的访问请求

### 4.4. 过滤器-登录校验逻辑

- 获取 url
- url 包含 login，**放行**。
- 获取 token
- 获取失败，**返回 40**1
- 获取成功
- 解析失败，**返回 401**
- 解析成功, **放行**。

登录和 token 解析成功，是放行。

token 获取或解析失败，是 401。


## 5. 拦截器

### 5.1. 拦截器使用步骤？

- 定义类实现接口 `handlerInterceptor`, 类用 `@Component` (定义自己拦截器组件)
	- preHandle 方法实现
	- postHandle 方法实现
	- afterHandle 方法实现
- 定义配置类实现接口 `WebMvcConfigurer`
	- 重写 addInterceptors 方法
	- 方法的拦截器注册对象
		- 添加自己的**拦截器对象**
		- 添加拦截器对象要**拦截的路径**

### 5.2. 拦截路径例子？

- /** 拦截任意路径
- /emps/** 拦截 emps 下任意路径
- /* 拦截一级路径
- /emps/* 拦截 emps 下的一级路径

```java
@Override  
public void addInterceptors(InterceptorRegistry registry) {  
    //注册自定义拦截器对象  
    registry.addInterceptor(demoInterceptor)  
            .addPathPatterns("/**")//设置拦截器拦截的请求路径（ /** 表示拦截所有请求）  
            .excludePathPatterns("/login");//设置不拦截的请求路径  
}

```

### 5.3. 拦截器和过滤器区别？

- 接口规范
	- **过滤器需要实现Filter接口**
	- **拦截器需要实现HandlerInterceptor接口。**
- 拦截范围
	- **过滤器Filter会拦截所有的资源**
	- **Interceptor只会拦截Spring环境中的资源。**

![assets/03-web/15-web实战-登录认证/IMG-20250531-223807-390.png](/img/user/assets/03-web/15-web%E5%AE%9E%E6%88%98-%E7%99%BB%E5%BD%95%E8%AE%A4%E8%AF%81/IMG-20250531-223807-390.png)

### 5.4. 拦截器-登录校验逻辑

和过滤器逻辑一样。

放行方式不同。
- 拦截器是 preHandle 里 return true;
- 过滤器是 chain. doFilter (req, resp)

```java
public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {  
    System.out.println("preHandle .... ");  
    return true; //true表示放行  
}
```


```java
import com.jun.utils.JwtUtils;  
import jakarta.servlet.*;  
import jakarta.servlet.annotation.WebFilter;  
import jakarta.servlet.http.HttpServletRequest;  
import jakarta.servlet.http.HttpServletResponse;  
import lombok.extern.slf4j.Slf4j;  
import org.apache.http.HttpStatus;  
import org.springframework.util.StringUtils;  
import java.io.IOException;  
  
@Slf4j  
@WebFilter(urlPatterns = "/*")  
public class TokenFilter implements Filter {  
    @Override  
    public void doFilter(ServletRequest req, ServletResponse resp, FilterChain chain) throws IOException, ServletException {  
        HttpServletRequest request = (HttpServletRequest) req;  
        HttpServletResponse response = (HttpServletResponse) resp;  
        String url = request.getRequestURL().toString();  
        if (url.contains("login")) {  
            log.info("登录请求 , 直接放行");  
            chain.doFilter(request, response);  
            return;        }  
        String jwt = request.getHeader("token");  
        if (!StringUtils.hasLength(jwt)) { //jwt为空  
            log.info("获取到jwt令牌为空, 返回错误结果");  
            response.setStatus(HttpStatus.SC_UNAUTHORIZED);  
            return;        }  
        try {  
            JwtUtils.parseJWT(jwt);  
        } catch (Exception e) {  
            e.printStackTrace();  
            log.info("解析令牌失败, 返回错误结果");  
            response.setStatus(HttpStatus.SC_UNAUTHORIZED);  
            return;        }  
        log.info("令牌合法, 放行");  
        chain.doFilter(request, response);  
    }  
}
```


```java
import com.jun.utils.JwtUtils;  
import jakarta.servlet.http.HttpServletRequest;  
import jakarta.servlet.http.HttpServletResponse;  
import lombok.extern.slf4j.Slf4j;  
import org.apache.http.HttpStatus;  
import org.springframework.stereotype.Component;  
import org.springframework.util.StringUtils;  
import org.springframework.web.servlet.HandlerInterceptor;  
  
@Slf4j  
@Component  
public class TokenInterceptor implements HandlerInterceptor {  
    @Override  
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {  
        String url = request.getRequestURL().toString();  
        if (url.contains("login")) { //登录请求  
            log.info("登录请求 , 直接放行");  
            return true;        }  
        String jwt = request.getHeader("token");  
        if (!StringUtils.hasLength(jwt)) { //jwt为空  
            log.info("获取到jwt令牌为空, 返回错误结果");  
            response.setStatus(HttpStatus.SC_UNAUTHORIZED);  
            return false;        }  
        try {  
            JwtUtils.parseJWT(jwt);  
        } catch (Exception e) {  
            e.printStackTrace();  
            log.info("解析令牌失败, 返回错误结果");  
            response.setStatus(HttpStatus.SC_UNAUTHORIZED);  
            return false;        }  
        log.info("令牌合法, 放行");  
        return true;    }  
}
```




> [!important]+ 
> 
> `@Order` 指定拦截器优先级，数字小，优先级高。
> 
> 适合拦截器是 Spring Bean 的场景（`@Order` 只有在拦截器以 Bean 的方式存在于 Spring 容器中时才生效）
> 
> 例子：
```java
@Component
@Order(1)
public class FirstInterceptor implements HandlerInterceptor {
    // ...
}

@Component
@Order(2)
public class SecondInterceptor implements HandlerInterceptor {
    // ...
}
```



```java

AFilter init
BFilter init
CFilter init
# 服务器启动的时候，filter的初始化执行一次 ----------------------


AFilter 放行前
BFilter 放行前
CFilter 放行前


TokenInterceptor preHandle 请求进入 Controller 之前执行

AController print...

TokenInterceptor postHandle Controller 执行后,视图渲染前执行
TokenInterceptor afterHandle 请求完成后执行（包括视图渲染完成之后）

CFilter 放行后
BFilter 放行后
AFilter 放行后

# 服务器关闭的时候，filter的销毁执行一次  ----------------------
CFilter destory
BFilter destory
AFilter destory
```

**视图渲染完成**理解：

- 视图解析器渲染视图（JSP/Thymeleaf等）
- 页面 HTML 渲染输出到客户端

或

- HttpMessageConverter 将对象转换为 JSON 并写入响应体。响应体输出完成（即 JSON 返回给前端）

[[03-web/14-web实战-学员管理-自\|上一节：14-web实战-学员管理-自]]

[[03-web/16-web实战-aop\|下一节：16-web实战-aop]]
