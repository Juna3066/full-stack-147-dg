---
{"dg-publish":true,"permalink":"/03-web/12-web实战-删除-修改/","dgPassFrontmatter":true}
---


## 1. 删除员工

前端传递值? ids=1,2,3 后端如何接受？

- 用数组
- 用集合
- sql 的 foreah

用来批量删除和批量删除公用一个接口。


## 2. 修改员工


自定义 resutlMap 封装复杂结果

```xml
<resultMap id="empRM" type="com.jun.entity.Emp">
<id column="" property="">
<result column="" property="">

<!--封装list-->
<collection property="exprList" offType="com.jun.entity.EmpExpr">
<id column="" property="">
<result column="" property="">
</Collection>

</resultMap>

```

更新：
- 明细表，先删除，再添加。
- 主子表，加事务。

## 3. 异常处理


全局异常处理器，统一异常返回结果。


```java
@Slf4j
@RestControllerAdvice
public class GlobalExceptionHandler {
@ExceptionHandler
public Result handleException(Exception e) {
log.error()
return Result.error("")
}

}

```

## 4. 员工信息统计


### 4.1. sql case 流程控制函数
```sql

case 
when con1 then res1 else res2
end;

case 
expr when val 1 then res 1 else res 2
end;

```


### 4.2. if 流程控制函数

```sql
if(expr,v1,v2) true 1 false 2
ifnull(expr,v1) Null v1 否则自己
```

查询结果向 map 封装，maper 接口可用@MapKey("name") 也可以不指定


[[03-web/11-web实战-新增员工\|上一节：11-web实战-新增员工]]

[[03-web/13-web实战-班级管理-自\|下一节：13-web实战-班级管理-自]]
