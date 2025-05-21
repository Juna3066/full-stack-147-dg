---
{"dg-publish":true,"permalink":"/03-web/07-web实战-数据库/","dgPassFrontmatter":true}
---


DBMS 数据库操作系统。


## 1. MySQL 的安装和连接


MySQL 有社区版和服务器版，一般用社区版 (免费)
版本 8.0.34

- 解压
- 配置环境变量（？）
- 初始化
- 注册服务
- 启动服务 `net start/stop mysql `
- 连接 `mysql -u root [-h ip: port] -p password`

## 2. 图形化工具

### 2.1. DataGrip 2024.3.3

- ctrl + enter 执行 SQL

## 3. 数据模型

- 关系型数据库
	- 有二维表组成。
- 非关系数据库

MySQL 默认有 4 个表，在 `data` 文件夹下，一个文件代表一个数据库。

## 4. SQL 分类

SQL 结构化查询语言
- DDL 数据库定义语言（库、表、字段相关操作）
- DML 数据库操作语言 (增删改)
- DQL 数据库查询语言 (查)
- DCL 数据库控制语言（控制用户的访问权限，DBA DB admin 数据库管理员的职责）

SQL 通用语法：
- 注释 `--  或 /* */`
- 分号结尾
- 不区分大小写
- 空格不影响 SQL，可以增强可读性


## 5. DDL

### 5.1. 数据库操作

```sql
show databases;
use db_xxx;
select database(); -- 当前数据库？
drop database [if exists] bd_xxx;
create database [if not exist] db_xxx [default charset utf8mb4] -- #TODO 

-- database 可替换 schema
-- MySQL8 默认使用字符集 utf8mb4 -- 联系 #TODO 
```



### 5.2. 表操作-创建表

```sql
create table tb_xxx(
字段1 type [约束][comment 注释内容] ,
字段2 type [约束][comment 注释内容]
);

-- 约束：not null, unique, primary key, auto increment, default, foreign key -- #TODO 

```

### 5.3. MySQL 数据类型

[[06-四方保险/01-项目介绍-环境搭建#3. 数据库建模\|Power Designer 上显示的标准数据类型]]

> [!important]+ 
> 
> 重点 

数据类型主要分为：
- 数值
	- unsigned tinyint
	- int
	- bigint
	- decimial (10,2)
- 日期
	- data
	- time
	- year
	- datetime
	- timestamp (1970-01-01 到 2038-01) #TODO 
- 字符串 (能定长度就定长)
	- char
	- varchar
	- txt
	- blog


### 5.4. 表操作-加约束创建表


### 5.5. DDL 操作案例

表一般都要有 `id, create_time, update_time`


### 5.6. 表操作-查找-修改-删除

```sql
show tables ;  
desc t_user;
drop table if exists t_user;
# 修改表结构 字段 类型[长度] [约束]
alter table t_user add column age int default 0 comment "年龄";
alter table t_user drop column age;
alter table t_user modify # 只修改数据类型和长度
alter table t_user # 如添加，修改所有
```

## 6. DML

### 6.1. 增

```sql
insert into table () values ()
select now();
字符串插入单引号都行。
```

### 6.2. 删

```sql
delete from t_xx where condition;
```

### 6.3. 改（更新）

```sql
update t_xx set x=v,x2=v2 where condition;
```

## 7. DQL

### 7.1. 基本查询

```sql
select * from t_xxx 
where condition
group by xx having  xx on xx
order by xx desc/asc
limit 0,10

select age as a 起别名

distinct
```

### 7.2. 条件查询
```sql
between 0 and 10  [0,10]
in(1,2,3)
like '___' # 一个占位符
like '%%' # 模糊查询
and &&
or ||
not !
is null
is not null
```

### 7.3. 聚合函数
```sql
count
max,min,avg,sum

null不参与聚合函数，例如：count(address) address是null的不会计数。
count(field)和count(*) 推荐后者，数据库底层做了优化。


```
### 7.4. 分组查询

### 7.5. 排序
```sql
score asc/desc  默认asc
```
### 7.6. 分页
```sql
分页是方言，第一页可以缩写。 
limit offset,count
limit 0,10 => limit 10  从偏移量0的位置开始，取10个数据。
公式  
offset=(page-1)*pageSize count=pageSize
limit (page-1)*pageSize,pageSize
```

### 总结


> [!important]+ 
> 
> 1.mysql 执行顺序
> 

```
步骤
select
	5字段列表
from
	表名 1
where
	2
group by
	3
having
	4分组后条件列表
order by
	6.排序列表
limit
	7.分页参数

```



[[03-web/06-web实战-ioc-di\|上一节：06-web实战-ioc-di]]

[[03-web/08-web实战-java操作数据库\|下一节：08-web实战-java操作数据库]]