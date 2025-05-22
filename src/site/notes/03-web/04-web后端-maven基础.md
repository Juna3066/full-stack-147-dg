---
{"dg-publish":true,"permalink":"/03-web/04-web后端-maven基础/","dgPassFrontmatter":true}
---


## 1. 简介

- **依赖管理**
- **项目构建**
	- 统一项目的目录结构

## 2. 概述

pom 是项目对象模型

仓库分类：
- 本地仓库
- 远程仓库（私服）
- 中央仓库

## 3. 安装

- 下载
- 解压
- `conf/setting.xml` 配置

```xml
# 配置本地仓库
# 配置远程仓库
# MAVEN_HOME配置
```

```cmd
mvn -v
```

## 4. IDEA 集成

### 4.1. Maven-全局配置

IDEA 退出项目，全局配置：
- maven
	- 位置
	- xml
	- 仓库位置
	- runner 配置jdk
- java compiler 配置 jdk
- 项目的字符集编码 utf-8

### 4.2. 创建 maven 项目

如果代码量很多，可先创建空项目。在添加模块，作为具体项目。
比如：web 有很多天的学习 demo，每天作为一个 module.

- 新建空项目
- 新建模块，设置名称，位置，坐标

### 4.3. 导入 maven 项目

**先复制**模块代码到项目，然后：
- 方式 1：右侧 maven 点击 `+`，选择 pom. xml
- 方式 2：项目文件 -> 导入模块 -> 选择项目目录，或 pom. xml

## 5. 依赖管理

### 5.1. 依赖配置

pom. xml 加依赖，可以从中央仓库查依赖。

添加完依赖，刷新一下，maven 右侧面板，依赖，可以看到加入的依赖 jar 包。

### 5.2. 依赖传递

直接依赖，间接依赖。

`excusions ` 排除依赖

IDEA 插件，maven helper, 右键 execlude 排除依赖。

### 5.3. 生命周期

3 套生命周期，互不干扰。
- clean:
- default: compile, test, package, install (安装到本地仓库)
- site:

同一套中，后面阶段的运行，他前面的也会被执行。

`mvn compile `

## 6. 单元测试
### 6.1. 介绍

负责：
- 测试工程师
- 甲方，验收测试的工作人员

单元测试：
- 白盒测试（知道代码的细节）
- 黑盒测试（不知道）
- 灰盒测试（知道模糊的细节）

### 6.2. 快速入门

引入依赖，使用注解@Test

test 文件夹；XXTest {
	@Test
	testXX (){
	}
}

maven 点 test, 点 package, 可以指向对用命令。
**类名去掉 Test，就测不**到了。


### 6.3. 常用注解

BeforeAll 初始化资源, Afterall 释放资源
BeforeEach 每个方法执行前，会执行。

参数化测试
```java
@ParameterizedTest
@ValueSource(string={})
@DisplayName() 别名
```

### 6.4. 断言

自己写，自己看，看被测试的方法，结果，和自己的预期，是否一样。

## 7. 依赖范围

![assets/03-web/04-web后端-maven基础/IMG-20250522-174411-106.png](/img/user/assets/03-web/04-web%E5%90%8E%E7%AB%AF-maven%E5%9F%BA%E7%A1%80/IMG-20250522-174411-106.png)

## 8. 依赖爆红问题解决

- 网络问题，依赖下载不完整，去
本地仓库的 `xxx.lastUpdated` 删了，才能重新下载。

lastUpdated 文件删除脚本
```cmd
del /s *.lastUpdated
```

- IDEA 缓存，重启清理缓存


[[03-web/03-web前端-vue基础\|上一节：03-web前端-vue基础]]

[[03-web/05-web后端-基础知识\|下一节：05-web后端-基础知识]]

[[03-web/18-web后端-maven高级\|关联：18-web后端-maven高级]]