---
{"dg-publish":true,"permalink":"/03-web/09-web实战-部门管理/","dgPassFrontmatter":true}
---


## 1. 接口开发

- 请求方式
- 请求路径
- 请求参数
- 响应结果

请求路径是 Controller 上的和方法上的拼接

路径上的参数，接受参数
- 原始的方式
- 注解@RequestParam
- 省略注解@RequestParam

@PathVariable

@RequestBody，请求体里的参数
	json 参数用它标注实体接受。

新增的时候，填充默认值。
- #{} 会生成预编译 sql，位置替换成? 把参数当成一个整体传入。
- ${} sql 会字符串拼接

更新的时候
- 动态 sql, 确保 null 参数，不更新。

### 1.1. 删除



### 1.2. 新增


### 1.3. 修改部门

- 回显
- 修改

## 2. 日志技术-logback

- springboot 项目不用引用 logback 的依赖，因为springboot 的依赖里包含了它。
- logback. xml 需要值的东西
	- log-level

使用 demo

[[03-web/08-web实战-java操作数据库\|上一节：08-web实战-java操作数据库]]

[[03-web/10-web实战-多表操作-员工列表查询\|下一节：10-web实战-多表操作-员工列表查询]]