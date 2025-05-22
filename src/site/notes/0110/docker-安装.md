---
{"dg-publish":true,"permalink":"/0110/docker-安装/","dgPassFrontmatter":true}
---


环境：anolis 8.10 

## docker

> [!cite]+ docker 参考文档
> https://docs.docker.net.cn/engine/install/
> https://docs.docker.net.cn/engine/install/centos/
> https://mirrors.tuna.tsinghua.edu.cn/help/docker-ce/
> https://github.com/dongyubin/DockerHub

```bash
# 安装 `dnf-plugins-core` 软件包（提供管理 DNF 仓库的命令）并设置仓库
sudo dnf -y install dnf-plugins-core
# 关闭防火墙,重要
sudo systemctl stop firewalld
# 添加cent仓库
sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
# 替换仓库中无法放问题的地址
sudo sed -i 's+https://download.docker.com+https://mirrors.tuna.tsinghua.edu.cn/docker-ce+' /etc/yum.repos.d/docker-ce.repo
# 安装
sudo dnf install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin --allowerasing
# 配置dockerhub的镜像仓库,解决官方镜像仓库无法访问的问题
mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<EOF
{
  "registry-mirrors": [
    "https://docker.1ms.run",
    "https://docker.mybacc.com",
    "https://dytt.online",
    "https://lispy.org",
    "https://docker.xiaogenban1993.com",
    "https://docker.yomansunter.com",
    "https://aicarbon.xyz",
    "https://666860.xyz",
    "https://docker.zhai.cm",
    "https://a.ussh.net",
    "https://hub.littlediary.cn",
    "https://hub.rat.dev",
    "https://docker.m.daocloud.io"
  ]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
# 开机启动
sudo systemctl enable --now docker
```


```bash
sudo systemctl enable --now docker
```

## portainer

> [!cite]+ portainer 参考文档
> https://docs.portainer.io/start/install-ce/server/docker/linux

## harbor

> [!cite]+ harbor 参考文档
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

