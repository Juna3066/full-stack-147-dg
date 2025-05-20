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

```

## 6. DML

### 6.1. 增

```sql

```

### 6.2. 删

```sql

```

### 6.3. 改（更新）

```sql

```

## 7. DQL

### 7.1. 基本查询

### 7.2. 条件查询

### 7.3. 聚合函数

### 7.4. 分组查询

### 7.5. 排序

### 7.6. 分页



[[03-web/06-web实战-ioc-di\|上一节：06-web实战-ioc-di]]

[[03-web/08-web实战-java操作数据库\|下一节：08-web实战-java操作数据库]]