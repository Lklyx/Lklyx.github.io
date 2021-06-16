---
title: 学习Docker
date: 2021/05/18
categories:
- [历练ing,扩展知识,Docker]
tags:
- Docker
---

# Docker 学习路径

学习视频地址[Docker](https://www.bilibili.com/video/BV1og4y1q7M4?p=1)

1. Docker概述
2. Docker安装
3. Docker命令
   - 镜像命令
   - 容器命令
   - 操作命令
4. Docker镜像！
5. 容器数据卷！
6. DockerFile
7. Docker网络原理
8. IDEA整合Docker
9. Docker Compose
10. Docker Swarm
11. CI、CD Jenkins

# Docker概述



…

# 安装Docker

> 准备环境

1. 需要会一点Linux的基础
2. CentOS 7 及以上版本
3. 我们使用Xshell连接远程服务器进行操作！

> 环境查看

```shell
# 系统内核是3.0以上的
uname -r
4.18.0-240.10.1.el8_3.x86_64
```

```shell
# 系统版本
[root@yanan sbin]# cat /etc/os-release 
NAME="CentOS Linux"
VERSION="8"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="8"
PLATFORM_ID="platform:el8"
PRETTY_NAME="CentOS Linux 8"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:8"
HOME_URL="https://centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"
CENTOS_MANTISBT_PROJECT="CentOS-8"
CENTOS_MANTISBT_PROJECT_VERSION="8"
[root@yanan sbin]# 
```

> 安装

查看官网的帮助文档：

```shell
# 1、卸载旧的版本
yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
# 2、需要的安装包
yum install -y yum-utils

# 3、设置镜像的仓库 使用国内阿里云的镜像仓库
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo

# 更新yum软件包的索引
yum makecache fast

# 4、安装docker相关的类容 docker-ce 社区版本 docker-ee 企业版
yum install docker-ce docker-ce-cli containerd.io

# 5、启动docker
systemctl start docker

# 6、使用docker version 查看是否安装成功。
docker version

# 7、hello-world
docker run hello-world
```

![image-20210616175154839](E:\Lklyx.github.io\source\_posts\Growth-Diary\扩展知识\Docker\image\1.png)

```shell
# 8、查看一下下载的这个 hello-world 镜像
docker images
```

### 了解：怎么卸载docker

```shell
# 1、卸载依赖
yum remove docker-ce docker-ce-cli containerd.io
# 2、删除docker资源
rm -rf /var/lib/docker
```

8
