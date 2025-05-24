---
{"dg-publish":true,"permalink":"/03-web/06-web实战-ioc-di/","dgPassFrontmatter":true}
---


#已实践

## 1. 初始化项目

因为 IDEA 创建 `springboot` 的版本高, 本地使用 `lombok` 报错。

可能是 pom. xml 的版本冲突问题。

- 因此用创建 maven 普通项目。
- pom. xml 添加依赖
	- 父依赖
	- 起步依赖
	- 其他
- application. yml
- 启动类

> [!important]+ 
> 使用的各种版本
> JDK 21 + SpringBoot 3.2

## 2. 完成 demo

restful 风格，一种软件架构风格。url 简洁、优雅。

完成接口 `/depts`

去读 resources 下的 depts, 返回前端。

- @RestController
	- @Controler + @RequestBody
- @RequestMapping
	- 可以指定方法
- @GetMapping
	- @RequestMapping 指定方法的简化写法。

## 3. 统一返回结构

方便前端操作。


## 4. 三层架构

代码分层，便于维护。

比如，业务变动，只用改 service 代码，其他两层不用变。

## 5. 扩展性

面向接口编程。

便于实现的切换。便于扩展。

## 6. 解耦

new 依赖关系强。

耦合，是指层，模块间的代码依赖性、关联性强。

推荐 `高内聚，低耦合`。

解决方案：
- 把需要的对象放入容器，用的时候，自动获取。

这正是 spring 容器的活。


- 控制反转
	- new 的工作给容器完成
	- @Componet 标记类，被容器管理，被标记的类，叫 bean。为了更好的标记不同层的 bean，衍生注解
		- @Controller (web 开发这个注解，不能用@Componet 替换)
		- @Service
		- @Repository
- 依赖注入
	- 用的时候，容器注入。
	- 情景 1
		- 用的对象的地方，@AutoWired
		- 容器中的名字，默认是类名开头小写。可以用@Service ("name") 指定
	- 情景 2
		- @Primay
		- 使用的对象的地方，@AutoWired
	- 情景 3
		- @Qualifier ("name")
		- @AutoWired
	- 4
		- @Resource (name="") 相当 3，这个注解是 JDK 提供的。

[[03-web/05-web后端-基础知识\|上一节：05-web后端-基础知识]]

[[03-web/07-web实战-数据库\|下一节：07-web实战-数据库]]
