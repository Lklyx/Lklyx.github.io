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

#  安装Docker

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

<img src="e:\Lklyx.github.io\source\_posts\Growth-Diary\扩展知识\Docker\image\1.png" alt="image-20210616175154839"  />

```shell
# 8、查看一下下载的这个 hello-world 镜像
docker images
```

## 了解：怎么卸载docker

```shell
# 1、卸载依赖
yum remove docker-ce docker-ce-cli containerd.io
# 2、删除docker资源
rm -rf /var/lib/docker
```

## 底层原理

**Docker是什么工作的？**

Docker是一个Client - Server结构的系统，Docker的守护进程运行在主机上

# Docker的常用命令

## 帮助命令

```shell
docker version # 查看docker的版本
docker info # 查看docker的更加详细信息
docker --help # 万能命令
```

帮助文档的地址：https://docs.docker.com/engine/reference/commandline/cli/

## 镜像命令

```shell
[root@yanan /]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
hello-world   latest    d1165f221234   3 months ago   13.3kB
# 解释
REPOSITORY 镜像的仓库源
TAG        镜像的标签
IMAGE ID   镜像的ID
CREATED    镜像的创建时间
SIZE       镜像的大小

# 可选性
-a， --all			# 列出所有镜像
-q， --quiet			# 只显示镜像ID
```

**docker search搜索镜像**

```shell
[root@yanan /]# docker search mysql
NAME                              DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
mysql                             MySQL is a widely used, open-source relation…   11003     [OK]       
mariadb                           MariaDB Server is a high performing open sou…   4169      [OK]      
......

# 可选性，通过搜索来过滤
--filter=STARS=3000 # 搜索出来的镜像就是STARS大于3000的
[root@yanan /]# docker search mysql --filter=STARS=3000
NAME      DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
mysql     MySQL is a widely used, open-source relation…   11003     [OK]       
mariadb   MariaDB Server is a high performing open sou…   4169      [OK] 
```

**docker pull 下载镜像**

```shell
# 下载镜像 docker pull + 镜像名 +[tag]版本号 	镜像名以后可以加下载版本。
[root@yanan /]# docker pull mysql
Using default tag: latest	# 如果不写tag版本。默认就是latest
latest: Pulling from library/mysql
69692152171a: Pull complete 	# 分层下载，docker image的核心 联合文件系统
1651b0be3df3: Pull complete 
951da7386bc8: Pull complete 
0f86c95aa242: Pull complete 
37ba2d8bd4fe: Pull complete 
6d278bb05e94: Pull complete 
497efbd93a3e: Pull complete 
f7fddf10c2c2: Pull complete 
16415d159dfb: Pull complete 
0e530ffc6b73: Pull complete 
b0a4a1a77178: Pull complete 
cd90f92aa9ef: Pull complete 
Digest: sha256:d50098d7fcb25b1fcb24e2d3247cae3fc55815d64fec640dc395840f8fa80969	# 签名
Status: Downloaded newer image for mysql:latest
docker.io/library/mysql:latest # 真实地址

# 等价于它
docker pull mysql
docker pull docker.io/library/mysql:latest
```

**docker rmi 删除镜像**

```shell
docker rmi -f + 容器id		# 删除指定的容器
docker rmi -f + 容器id + 容器id + 容器id		#删除多个容器
docker rmi -f $(docker images -aq)		# 删除全部的容器。
```

## 容器命令

> 说明：我们有了镜像才可以创建容器，linux，下载一个Cent OS镜像来测试学习。

```shell
docker pull centos
```

**新建容器并启动**

```shell
docker run [可选参数] image
# 参数说明
--name="Name"		容器名字 tomcat1，tomcat2，用来区分容器
-d				后台方式运行
-it				使用交互方式运行
-P			大写P	指定容器的端口 -p 8080:8080。有以下四种方式
	-P ip:主机端口:容器端口
	-P 主机端口:容器端口 （常用）
	-P 容器端口
	容器端口
-p			小写p	随机指定端口

# 测试 启动并进入容器
[root@yanan /]# docker run -it centos /bin/bash
# 解释：启动docker run ，使用it交互方式运行，运行centos。linux中，控制台一般是在/bin目录下面，bin目录下面，使用bash命令。
[root@9456c976569b /]# ls
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var

# 退出容器命令
exit
```

**列出所有运行中的容器**

```shell
# docker ps	命令
-a # 列出当前正在运行的容器 + 带出历史运行记录。
-n=？ # 显示最近创建的容器。登录？？？等于一，就是显示一条。
-q # 只显示容器的编号
```

**退出容器**

```shell
exit   # 直接容器停止并退出
Ctrl + p + Q	# 容器不停止退出
```

**删除容器**

```shell
docker rm 容器id		# 删除指定的容器，不能删除正在运行的容器，如果要强制删除 rm -f
docker rm -f $(docker ps -aq)	# 强制删除所有容器。
docker ps -a -q | xargs docker rm	#删除所有的容器。
```

**启动和停止容器的操作**

```shell
docker start 容器id	# 启动容器
docker restart 容器id	# 重启容器
docker stop 容器id	# 停止当前正在运行的容器
docker kill 容器id	# 停止当前正在运行的容器
```

