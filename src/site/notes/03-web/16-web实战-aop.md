---
{"dg-publish":true,"permalink":"/03-web/16-web实战-aop/","dgPassFrontmatter":true}
---


## AOP 程序的开发步骤？

1. 引入依赖
2. 编写 AOP 程序（公共的代码逻辑）
	1. @Aspect + @Component
	2. @Around

## Spring AOP 的应用场景？

1. 记录系统的操作日志
2. 事务管理
3. 权限控制


## AOP 的核心概念有哪些？


- 切面类 @Aspect + @Component
- 通知@Around, 公共性的功能。
- 目标对象，通知应用的对象。
	- （ServiceImpl 对象）
- 连接点，可以被 AOP 控制的方法。
	- （ServiceImpl 对象里的方法）
- 切入点，
	- 通知注解@Around 里切入点表达式匹配到的连接点。（ServiceImpl 匹配到切入点表达式的对象里的方法）


## AOP 的执行流程是什么？

在管理 bean 对象的过程中，框架通过底层的**动态代理**机制，程序员对特定的方法编程，增强功能。


## 常见的通知类型有哪些？

1. @Before，前置通知
2. @After，后置通知
3. **@Around**，环绕通知
	1. 需要调用 ProceedingJoinPoint. proceed (), 让原来的方法执行。
	2. 方法的返回值必须是 Object, 来接受原始方法的返回值。
4. AfterReturning，返回后通知
5. AfterThrowing，异常后通知


## @PointCunt 注解作用？

抽取公共的切入点表达式，提高复用性。


## execution 切入点表达式的完整语法？

## 可用的通配符有哪些？

- `*` 单个独立的任意符号
- `..` 多个连续的任意符号

## 书写建议有哪些？

- 业务方法名的命名应该规范，便于切入点表达式的快速匹配。`updateXXX`
- 通常基于接口描述切入点方法，增强拓展性。
- 在满足业务需求的前提下，尽量缩小切入点的匹配范围。
	- 包名尽量不使用 `..`，使用 `*` 匹配单个包

## `@annotaion` 切入点表达式的写法？

```java

```

## execution 切入点表达式和@annotation 切入点表达式的应用场景？

**切入点方法**
- 容易描述，用 execution 切入点表达式
- 不容易描述，用@annotation 切入点表达式

## JoinPoint 连接点的注意事项？
- 用来获**取目标的信息**
	- 类名
	- 方法名
	- 方法参数等
- **@Around 通知**，只能用 **ProceedingPoinPoint**
- 其他 4 个通知，只能用 JoinPoint
- JoinPoint 是 ProceedingPoinPoint 的父类。



[[03-web/15-web实战-登录认证\|上一节：15-web实战-登录认证]]

[[03-web/17-web后端-spring-boot原理\|下一节：17-web后端-spring-boot原理]]
