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

## 5. 数据卷-案例 2

## 6. Dockerfile 简介

## 7. Dockerfile 案例

## 8. Docker 网络

## 9. 项目部署-Java 应用部署

## 10. 项目部署-前端

## 11. Docker Compose 简介


## 12. Docker Compose 案例



[[05-微服务/01-mybatis-plus\|上一节：01-mybatis-plus]]

[[05-微服务/03-spring-cloud-基础\|下一节：03-spring-cloud-基础]]