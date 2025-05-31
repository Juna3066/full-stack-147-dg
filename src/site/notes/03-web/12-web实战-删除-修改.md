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


### @MapKey


```
@MapKey("columnName")
作用
把：
List<Map<String,Oject>> //String是key sql的column名字 Object是column名的值
转为 
Map<Object,Map<String,Oject>> //多出的Object key是注解指定的columnName


正常遍历
List<Map<String,Oject>>


快速索引获取用@MapKey("columnName")获取Map<Object,Map<String,Oject>>

```

| 类型                        | key 来源         | value 类型       | 常用场景           |
| --------------------------- | ---------------- | ---------------- | ------------------ |
| `Map<Object, Map>`          | SQL 中某列的值   | 一行数据的 KV 表 | 报表统计、简单查询 |
| `Map<Object, Entity>`       | 实体中某字段的值 | 单个实体对象     | 数据缓存、索引     |
| `Map<Object, List<Entity>>` | 分组字段的值     | 分组后的实体集合 | 分组列表、树状结构 |
| 


```java
public interface EmpMapper {

    @MapKey("deptId") // 使用 deptId 作为分组 key
    Map<Integer, List<Employee>> selectEmpGroupByDept();
}

```

```xml
<mapper namespace="com.example.mapper.EmpMapper">

    <!-- 映射 Employee 实体 -->
    <resultMap id="EmpResultMap" type="com.example.entity.Employee">
        <id     property="id"     column="id"/>
        <result property="name"   column="name"/>
        <result property="gender" column="gender"/>
        <result property="deptId" column="dept_id"/>
    </resultMap>

    <!-- 按部门分组返回员工列表 -->
    <select id="selectEmpGroupByDept" resultMap="EmpResultMap">
        SELECT id, name, gender, dept_id
        FROM emp
        ORDER BY dept_id
    </select>
</mapper>


```

结果

```
{
  1: [ {id: 1, name: "张三", deptId: 1}, {id: 2, name: "李四", deptId: 1} ],
  2: [ {id: 3, name: "王五", deptId: 2} ]
}
```