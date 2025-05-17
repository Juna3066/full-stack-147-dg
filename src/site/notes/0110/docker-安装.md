---
{"dg-publish":true,"permalink":"/0110/docker-安装/","dgPassFrontmatter":true}
---


环境：anolis 8.10 


> [!info]+ docker
> https://docs.docker.net.cn/engine/install/
> https://docs.docker.net.cn/engine/install/centos/
> https://mirrors.tuna.tsinghua.edu.cn/help/docker-ce/
> https://github.com/dongyubin/DockerHub


```bash
sudo systemctl enable --now docker
```

> [!info]+ portainer
> https://docs.portainer.io/start/install-ce/server/docker/linux

> [!info]+ harbor
> https://goharbor.io/docs/2.0.0/install-config/download-installer/

- 配置 Docker 的 `/etc/docker/daemon. json` 来信任 Harbor 私有仓库时，在 `insecure-registries` 中需要包含协议（即 `http://`）吗？
```bash
# 不需要协议,只需要 "host:port" 形式即可
# 如果你的 Harbor 是用 HTTP 部署（未使用 TLS/HTTPS），就必须添加到 "insecure-registries" 中，Docker 才允许与其通信
{
  "insecure-registries": [
    "harbor.local:5000"
  ]
}

# 1.修改 `/etc/docker/daemon.json`
# 2.重启 Docker 服务
sudo systemctl daemon-reexec
sudo systemctl restart docker
```
- hostname
- https 注释
- 初始登录密码

