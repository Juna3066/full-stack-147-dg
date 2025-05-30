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

[[03-web/08-web实战-java操作数据库\|上一节：08-web实战-java操作数据库]]

[[03-web/10-web实战-多表操作-员工列表查询\|下一节：10-web实战-多表操作-员工列表查询]]