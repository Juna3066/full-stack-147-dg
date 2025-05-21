---
{"dg-publish":true,"permalink":"/05-微服务/02-docker/","dgPassFrontmatter":true}
---


## 1. 快速入门

```bash
docker run -d --name mysql8 -p 3306:3306 \
-e TZ=Asia/Shanghai -e MYSQL_ROOT_PASSWORD=root mysql

docker load -i  xxx.jar
```

虚拟机建议挂起

- 容器
- 镜像
- `-p 宿主机端口号:容器端口号`
- 镜像名的组成？ `[rep][tag]`

## 2. 入门命令解读

```bash

systemctl status/start/stop/restart/enable docker

mkdir -p /etc/docker
cd mkdir 
vi daemon.json

# 配置镜像仓库加速地址
# 重新加载配置文件
systemctl daemon-reload
systemctl restart doceker
```

windows 上和虚拟机上，推荐虚拟机上更方便，我思考？
- 占用电脑内存
- 虚拟机可快照

## 3. 常见命令

```bash
# 通过dockerfile文件制作镜像
docker build 
docker save -o
docker load -i
docker pull/push/images/rmi
docker logs/run/stop/start/ps/rm
# docker进入容器，并使用指定终端和容器交互
docker exec -it nginx /bin/bash
```

## 4. 数据卷

- volume
- 是容器目录到宿主机目录的**映射桥梁**

```bash

docker volume create/ls/rm/inspect/prune

-v 数据卷:容器目录
-v html:/usr/share/nginx/html
```

## 5. 数据卷-案例 2

官方镜像仓库查 mysql。

使用数据目录，配置文件，初始化脚本放挂在目录，基于宿主机目录实现。

```bash
docker inspect 容器名

# 创建容器时候的参数
-v /root/mysql/data:/var/lib/mysql
-v /root/mysql/init:/docker-entrypoint-initdb.d
-v /root/mysql/conf:/etc/mysql/conf.d

# 查看mysql的字符集 编码表
show variables like '%char%'

```

[[10-anolis/基础必学课程/6.1-目录结构信息\|关联：linux的目录结构]]

## 6. Dockerfile 简介

部署 java 应用步骤
- 准备 linux, 安装 jre，配置环境变量；
- 复制 jar
- 运行脚本

镜像的结构是分层的，一层一层的。为了复用，提高利用率。拉去效率。
`docker build -t m:1.0 .`

## 7. Dockerfile 案例
```bash
FROM openjdk
ENV
COPY
RUN
ENTRYPOINT
```

## 8. Docker 网络

所有容器用 bridge 桥接的方式连接在 **docker 的一个虚拟网桥上**。

容器重启后 id 会变化。解决这个问题，用到它。

```bash
docker network --help
docker network create hmall
docker network connect hmall 容器名
docker inspect 容器名
docekr network connect --alias db hmall 容器名 #TODO 

进入容器内部，ping同一个docker网络下的容器，用容器名。
容器内的java应用的yml也可以写容器名了
```

## 9. 项目部署-Java 应用部署

```bash
docker run ... --network xxx
docker logs -f ...
```

## 10. 项目部署-前端

放 nginx 里，改代理配置。

## 11. Docker Compose 简介

组件容器，手动命令，一个一个启动，的解决方案：`docker-compose. yml`

定义一组关联的容器，实现多个关联 `depends_on:` 容器的快速部署。


```bash
docker compose [option] [cmd] 
-f/p
up/down/ps/logs/stop/start/restart/top/exec
```

## 12. Docker Compose 案例

```bash
docker rm -f ${docker ps -qa}
docker network rm hmall
docker compose up -d
```

[[05-微服务/01-mybatis-plus\|上一节：01-mybatis-plus]]

[[05-微服务/03-spring-cloud-基础\|下一节：03-spring-cloud-基础]]