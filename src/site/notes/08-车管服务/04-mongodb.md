---
{"dg-publish":true,"permalink":"/08-车管服务/04-mongodb/","dgPassFrontmatter":true}
---


> 参考资料 https://www.runoob.com/mongodb/mongodb-tutorial.html

## 1. 简介

官网：[http://www.mongodb.org/](http://www.mongodb.org/)

MongoBD 是一个**跨平台**的、**面向文档**的、**非关系型**的 数据库。文件存储格式是 BSON (一种JSON的扩展)

MongoDB 的逻辑结构 3部分组成：
- 文档 document (类似 关系型数据库的 一行记录 row)
- 集合 collection (类似 关系型数据库的 表 table)
- 数据库 database (类似 关系型数据库的 数据库 database)

目前以使用过数据库：
- MySQL **关系型数据库 (RDBMS)**
- Redis **键值存储 (Key-Value Store)**
- Elasticsearch **搜索引擎数据库 (Search Engine Database)**
- InfluxDB **时间序列数据库 (Time-Series Database, TSDB)**
- MongoDB **文档数据库 (Document Database)**

## 2. 安装、启动、连接

### 2.1. 下载版本
- 官网最新是 8.x
- 当前安装 6.0.23

下载地址 https://www.mongodb.com/try/download/community

![assets/08-车管服务/04-mongodb/IMG-20250510-181805-038.png](/img/user/assets/08-%E8%BD%A6%E7%AE%A1%E6%9C%8D%E5%8A%A1/04-mongodb/IMG-20250510-181805-038.png)

### 2.2. 安装

#### 2.2.1. 点击安装包

mongodb-windows-x86_64-6.0.23-signed.msi 开始安装

![assets/08-车管服务/04-mongodb/IMG-20250510-160334-020.png](/img/user/assets/08-%E8%BD%A6%E7%AE%A1%E6%9C%8D%E5%8A%A1/04-mongodb/IMG-20250510-160334-020.png)

#### 2.2.2. 同意协议

![assets/08-车管服务/04-mongodb/IMG-20250510-160351-283.png](/img/user/assets/08-%E8%BD%A6%E7%AE%A1%E6%9C%8D%E5%8A%A1/04-mongodb/IMG-20250510-160351-283.png)

#### 2.2.3. 选择自定义安装

![assets/08-车管服务/04-mongodb/IMG-20250510-160516-199.png](/img/user/assets/08-%E8%BD%A6%E7%AE%A1%E6%9C%8D%E5%8A%A1/04-mongodb/IMG-20250510-160516-199.png)

#### 2.2.4. 设置安装位置

![assets/08-车管服务/04-mongodb/IMG-20250510-160547-281.png](/img/user/assets/08-%E8%BD%A6%E7%AE%A1%E6%9C%8D%E5%8A%A1/04-mongodb/IMG-20250510-160547-281.png)

#### 2.2.5. 安装 MongoDB服务

安装 MongoDB服务作为网络服务。设置服务名称、数据目录、日志目录

![assets/08-车管服务/04-mongodb/IMG-20250510-174434-611.png](/img/user/assets/08-%E8%BD%A6%E7%AE%A1%E6%9C%8D%E5%8A%A1/04-mongodb/IMG-20250510-174434-611.png)

#### 2.2.6. 安装MongoDB Compass

MongoDB 官方提供的一款 **图形化界面（GUI）工具**。如果没自动安装成功。可手动[下载](https://www.mongodb.com/products/tools/compass)安装。

或者不安装，使用其他图形化工具。

![assets/08-车管服务/04-mongodb/IMG-20250510-174502-648.png](/img/user/assets/08-%E8%BD%A6%E7%AE%A1%E6%9C%8D%E5%8A%A1/04-mongodb/IMG-20250510-174502-648.png)

#### 2.2.7. 点击install

![assets/08-车管服务/04-mongodb/IMG-20250510-174521-038.png](/img/user/assets/08-%E8%BD%A6%E7%AE%A1%E6%9C%8D%E5%8A%A1/04-mongodb/IMG-20250510-174521-038.png)

#### 2.2.8. 完成安装

![assets/08-车管服务/04-mongodb/IMG-20250510-174616-295.png](/img/user/assets/08-%E8%BD%A6%E7%AE%A1%E6%9C%8D%E5%8A%A1/04-mongodb/IMG-20250510-174616-295.png)

### 2.3. 启动

安装完成后，无需操作，服务默认是已经启动的。

![assets/08-车管服务/04-mongodb/IMG-20250510-183541-237.png](/img/user/assets/08-%E8%BD%A6%E7%AE%A1%E6%9C%8D%E5%8A%A1/04-mongodb/IMG-20250510-183541-237.png)

### 2.4. 连接

用 DataGrip 连接 MongoDB

URL:`mongodb://localhost:27017`

![assets/08-车管服务/04-mongodb/IMG-20250510-190639-335.png](/img/user/assets/08-%E8%BD%A6%E7%AE%A1%E6%9C%8D%E5%8A%A1/04-mongodb/IMG-20250510-190639-335.png)


## 3. 语法练习

```
// 语法帮助  
help;  
// 1.数据库  
show dbs;  
use db_full_stack_147  
db.dropDatabase();  
db;  
  
// 2.集合  
show collections;  
db.user.drop();  
  
// 3.文档  
// 增  
db.user.insertOne(  
    {name:"小小",age:5,sex:"男",address:"洛阳",phone:"16600001111",id_card:null}  
);  
db.user.insertMany([  
    {name:"小张三",age:10,sex:"男",address:"洛阳",phone:"16600002600",id_card:"0001"},  
    {name:"张三",age:13,sex:"男",address:"洛阳",phone:"16600002601",id_card:"0002"},  
    {name:"大张三",age:15,sex:"男",address:"洛阳",phone:"16600002602",id_card:"0002"},  
    {name:"李四",age:15,sex:"女",address:"杭州",phone:"166000000002692"},  
    {name:"王五",age:16,sex:"女",address:"杭州",phone:"15500002693"},  
    {name:"赵六",age:20,sex:"男",address:"郑州",phone:"15500002694"},  
    {name:"孙七",age:30,sex:"男",address:"郑州",phone:"15500002695"},  
]);  
  
// 删  
db.user.deleteOne({name:"小小"})  
db.user.deleteMany({age:{$gt:20}})  
  
// 改  
db.user.updateOne({name:"张三"},{$set:{name:"小张三",age:25}})  
db.user.updateMany({address:"郑州"},{$set:{address:"郑州市"}})  
  
// 查  
db.user.findOne()  
db.user.find();  
db.user.find({sex:"男"})  
// $eq  
db.user.find({sex:{$eq:"男"}})  
// $ne  
db.user.find({sex:{$ne:"男"}})  
//$gt $gte $lt $lte  
db.user.find({age:{$gt:15}})  
db.user.find({age:{$gte:15}})  
  
// $regex  类似 %张%  
db.user.find({name:/张/})  
db.user.find({name:{$regex:/张/}})  
// 以张开头 类似 张%  
db.user.find({name:/^张/})  
  
// null  
db.user.find({id_card:null})  
//$exists $in  
db.user.find({id_card:{$exists:true}})  
db.user.find({address:{$in:["郑州","洛阳"]}})  
  
//$or $and  
db.user.find({$or:[{address:"郑州"},{address:"洛阳"}]})  
db.user.find({$and:[{age:{$gt:10}},{age:{$lt:20}}]});
```

### 3.1. 数据库

![assets/08-车管服务/04-mongodb/IMG-20250510-202517-923.png](/img/user/assets/08-%E8%BD%A6%E7%AE%A1%E6%9C%8D%E5%8A%A1/04-mongodb/IMG-20250510-202517-923.png)

### 3.2. 集合

![assets/08-车管服务/04-mongodb/IMG-20250510-202529-888.png](/img/user/assets/08-%E8%BD%A6%E7%AE%A1%E6%9C%8D%E5%8A%A1/04-mongodb/IMG-20250510-202529-888.png)

### 3.3. 文档

![assets/08-车管服务/04-mongodb/IMG-20250510-202804-391.png](/img/user/assets/08-%E8%BD%A6%E7%AE%A1%E6%9C%8D%E5%8A%A1/04-mongodb/IMG-20250510-202804-391.png)

## 4. Java 操作 MongoDB 

资料
