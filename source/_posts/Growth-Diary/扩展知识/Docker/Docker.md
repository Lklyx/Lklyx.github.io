---
  title: 学习Docker
date: 2021/05/18
categories:
- [历练ing,扩展知识,Docker]
tags:
- Docker
---

# 常用命令

> 1. Docker容器信息
>
>    ```shell
>    ##查看docker容器版本
>    docker version
>    ##查看docker容器信息
>    docker info
>    ##查看docker容器帮助
>    docker --help
>    ```
>
> 2. 镜像操作
>
>    ```shell
>    # 查看本地所有镜像
>    docker images 
>
>    # 启动并进入镜像
>     docker run -it + 镜像名字：版本号 + /bin/bash
>    # 如果只加名字，就默认下载最新版本的启动
>
>    # 第一次启动镜像
>     docker run -d -p 3310:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql
>     -d # 后台运行
>     -p # 3310:3306 暴露端口
>     -v # 挂载数据，自动备份、路径
>     /home/mysql/conf:/etc/mysql/conf.d  这是映射配置文件的。
>     /home/mysql/data:/var/lib/mysql	这是映射配置数据文件的。
>
>    # 显示镜像ID
>    docker images -a
>    docker images -aq
>
>    # 搜索仓库MySQL镜像
>    docker search mysql
>
>    # 下载Redis官方最新镜像，相当于：docker pull redis:latest
>    docker pull redis
>
>    # 下载仓库所有Redis镜像
>    docker pull -a redis
>
>    # 下载私人仓库镜像
>    docker pull bitnami/redis
>
>    # 单个镜像删除，相当于：docker rmi redis:latest
>    docker rmi redis
>
>    # 强制删除(针对基于镜像有运行的容器进程)
>    docker rmi -f redis
>
>    # 删除本地全部镜像
>    docker rmi -f $(docker images -q)
>    ```
>
> 3. 容器的操作
>
>    ```shell
>       # 查看正在运行的容器
>       docker ps
>    
>       # 显示所有的容器，包括未运行的
>       docker ps -a
>    
>       # 启动容器
>       docker start 容器id	
>    
>       # 进入正在运行的命令行
>       docker exec -it + 容器id /bin/bash
>       docker attach 容器id	
>    
>       # 运行并进入容器。  使用exit退出，或者ctrl+p+q，退出。
>       docker run -it + 容器ID + /bin/bash
>    
>       # 强制删除已经启动的容器
>       docker rm -f + ID
>    
>       # 强制删除所有已经启动的容器。
>       docker rm -f $(docker ps -aq)
>       
>       # 删除容器中没有运行的容器
>       sudo docker rm $(sudo docker ps -aq)
>    
>       # 列出容器中的进程
>       docker top + ID
>    
>       # 查看容日的日志
>       docker logs -f -t --tail=5 + ID
>       # -f 跟踪日志输出
>       # -t 显示时间戳
>       # --tail=N 列出最新的 N 条内容。
>    
>       # 查看容器tomcat从2021年04月21日后的最新3条日志。
>       docker logs --since="2021-04-21" --tail=3 5afc660a7c3d
>    
>       docker restart 容器id	# 重启容器
>       docker stop 容器id	# 停止当前正在运行的容器
>       docker kill 容器id	# 杀死当前正在运行的容器
>    ```
>
> 4. 其他扩展
>
>    ```shell
>    # 查看容器的日志
>    docker logs -f -t --tail 容器ID
>    -f # 跟随最新的日志打印
>    -t # 是加入的时间戳
>    --tail # 显示最后多少条
>    ```
>
> 
>
> 

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

## 设置自动启动

```shell
systemctl enable docker.service
```

## 帮助命令

```shell
docker version # 查看docker的版本
docker info # 查看docker的更加详细信息
docker --help # 万能命令
```

帮助文档的地址：https://docs.docker.com/engine/reference/commandline/cli/

## 镜像命令

**docker images** 查看所有本地的主机上的镜像。

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
docker run [可选参数] images
# 参数说明
--name="Name"		 容器名字 tomcat1，tomcat2，用来区分容器
-d					后台方式运行
-it					使用交互方式运行
-P					大写P	指定容器的端口 -p 8080:8080。有以下四种方式
	-P ip:主机端口:容器端口
	-P 主机端口:容器端口 （常用）
	-P 容器端口
	容器端口
-p			小写p	随机指定端口

# 测试 启动并进入容器
[root@yanan /]# docker run -it centos /bin/bash
# 解释：启动docker run ，使用it交互方式运行，运行centos。linux中，控制台一般是在/bin目录下面，bin目录下面，使用bash命令运行。
[root@9456c976569b /]# ls
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var

# 退出容器命令
exit
Ctrl p Q
```

**列出所有运行中的容器**

```shell
# docker ps	命令
-a # 列出当前正在运行的容器 + 带出历史运行记录。
-n=？ # 显示最近创建的容器。？等于一，就是显示一条。
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

## 常用的其他命令

**后台启动容器**

```shell
# 命令 docker run -d + 镜像名
docker run -d centos
# 问题docker ps，发现了centos停止了。
# 常见的坑，docker容器使用后台运行，就必须要有一个前台进程，docker发现没有应用，就自动停止
# nginx，容器启动后，发现自己没有提供服务，就立刻停止，就是没有程序了。
```

**查看日志**

```shell
docker logs -f -t --tail 10	+ 容器id，没有日志
# 自己编写一段shell脚本
[root@yanan ~]# docker run -d centos /bin/sh -c "while true;do echo yanan;sleep 1;done"

[root@yanan ~]# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED             STATUS             PORTS     NAMES
632215a985f8   centos    "/bin/sh -c 'while t…"   2 minutes ago       Up 2 minutes                 fervent_sutherland
9625ad394ea0   centos    "/bin/bash"              About an hour ago   Up About an hour             silly_perlman
# 这里的id为632215a985f8这个的就是刚才上面我们自己编写的shell脚本。

# 显示日志
-tf
--tail number  # number 是要显示的条数。
[root@yanan ~]# docker logs -tf --tail 10 632215a985f8 

```

**查看容器中进程信息**

```shell
# 命令 docker top + 容器id
[root@yanan ~]# docker top 632215a985f8
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
root                130102              130082              0                   10:46               ?                   00:00:00            /bin/sh -c while true;do echo yanan;sleep 1;done
root                130980              130102              0                   10:56               ?                   00:00:00            /usr/bin/coreutils --coreutils-prog-shebang=sleep /usr/bin/sleep 1

```

**查看镜像的元数据**

```shell
# 命令
docker inspect + 容器id
# 例子如下：
[root@yanan ~]# docker inspect 632215a985f8
[
    {
        "Id": "632215a985f86604fb0140c1cccfb91d218abaa0b97e143cb70868148beab7fd",
        "Created": "2021-06-18T02:46:48.189412678Z",
        "Path": "/bin/sh",
        "Args": [
            "-c",
            "while true;do echo yanan;sleep 1;done"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 130102,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2021-06-18T02:46:48.519148447Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:300e315adb2f96afe5f0b2780b87f28ae95231fe3bdd1e16b9ba606307728f55",
        "ResolvConfPath": "/var/lib/docker/containers/632215a985f86604fb0140c1cccfb91d218abaa0b97e143cb70868148beab7fd/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/632215a985f86604fb0140c1cccfb91d218abaa0b97e143cb70868148beab7fd/hostname",
        "HostsPath": "/var/lib/docker/containers/632215a985f86604fb0140c1cccfb91d218abaa0b97e143cb70868148beab7fd/hosts",
        "LogPath": "/var/lib/docker/containers/632215a985f86604fb0140c1cccfb91d218abaa0b97e143cb70868148beab7fd/632215a985f86604fb0140c1cccfb91d218abaa0b97e143cb70868148beab7fd-json.log",
        "Name": "/fervent_sutherland",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "host",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/de124c2876dc50d329be43cecdffa6bb6687e99e5fa8623c0ea2c618387c821a-init/diff:/var/lib/docker/overlay2/99d95899194b53d6ee714912494fc15576f0712ab2077192fe7061696325fe9d/diff",
                "MergedDir": "/var/lib/docker/overlay2/de124c2876dc50d329be43cecdffa6bb6687e99e5fa8623c0ea2c618387c821a/merged",
                "UpperDir": "/var/lib/docker/overlay2/de124c2876dc50d329be43cecdffa6bb6687e99e5fa8623c0ea2c618387c821a/diff",
                "WorkDir": "/var/lib/docker/overlay2/de124c2876dc50d329be43cecdffa6bb6687e99e5fa8623c0ea2c618387c821a/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "632215a985f8",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
                "while true;do echo yanan;sleep 1;done"
            ],
            "Image": "centos",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "org.label-schema.build-date": "20201204",
                "org.label-schema.license": "GPLv2",
                "org.label-schema.name": "CentOS Base Image",
                "org.label-schema.schema-version": "1.0",
                "org.label-schema.vendor": "CentOS"
            }
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "b74dbfc943b00745c34506e0c5e60da5115ef4cf1939be0f00a436044db9d0dc",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {},
            "SandboxKey": "/var/run/docker/netns/b74dbfc943b0",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "5a814cb0d1f0e15c7cdd6b4c12d0ad0694e6c024b8b21af3ed8efecdd51bd312",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.3",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:03",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "cbf06a0493948171fe26ac9eb31e2584bac17d1aa55715470a3f478591125a77",
                    "EndpointID": "5a814cb0d1f0e15c7cdd6b4c12d0ad0694e6c024b8b21af3ed8efecdd51bd312",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.3",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:03",
                    "DriverOpts": null
                }
            }
        }
    }
]

```

**进入当前正在运行的容器**

```shell
# 我们通常容器都是使用后台方式运行的，需要进入容器，修改一些配置
# 命令
docker exec -it + 容器id /bin/bash
# 测试例子：
[root@yanan ~]# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED             STATUS             PORTS     NAMES
632215a985f8   centos    "/bin/sh -c 'while t…"   25 minutes ago      Up 25 minutes                fervent_sutherland
9625ad394ea0   centos    "/bin/bash"              About an hour ago   Up About an hour             silly_perlman
[root@yanan ~]# docker exec -it 9625ad394ea0 /bin/bash
[root@9625ad394ea0 /]# ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 01:43 pts/0    00:00:00 /bin/bash
root          16       0  0 03:12 pts/1    00:00:00 /bin/bash
root          30      16  0 03:13 pts/1    00:00:00 ps -ef

# 方式二
docker attach + 容器id

# docker exec		# 进入容器后开启一个新的终端，可以在里面操作（刚创建的容器）
# docker attach		# 进入容器正在执行的终端，不会启动行的进程（正在运行的容器）

```

**从容器内拷贝文件到主机上**

```shell
docker cp + 容器id：容器内路径	目的的主机路径
# 查看当前主机的进程
[root@yanan home]# docker ps
CONTAINER ID   IMAGE     COMMAND       CREATED         STATUS         PORTS     NAMES
dd3b2ccc9c13   centos    "/bin/bash"   3 minutes ago   Up 3 minutes             xenodochial_taussig

# 进入docker容器内部在容器内建一个文件
[root@yanan home]# docker attach dd3b2ccc9c13
[root@dd3b2ccc9c13 home]# touch test.java
[root@dd3b2ccc9c13 home]# ls  
test.java
[root@dd3b2ccc9c13 home]# exit
exit
# 将文件拷贝到我们的主机上。
[root@yanan home]# docker cp dd3b2ccc9c13:/home/test.java /home
# docker cp 容器id: + 需要拷贝的文件路径 + 需要拷贝的主机目录（这里是/home）。
[root@yanan home]# ls
test.java  yanan.java

#拷贝是一个手动过程，未来我们使用 -v 卷的技术，可以实现，自动同步，主机上的/home  和  容器上的/home 、自动备份。
```

## 练习

> Docker 安装 Nginx

```shell
# 搜索镜像 search 建议去docker官网搜索，可以看到帮助文档
# 下载镜像	pull
# 运行测试 
docker pull nginx
docker run -d --name nginx01 -p 3344:80 nginx
# 注释：使用docker运行下载的docker --name，是给镜像命名，默认的话， 不用写。这里给他重命为nginx01。-p，暴露一个端口号，暴露一个3344的端口号。后面加上nginx。启动nginx
# -d 后台运行
# --name	给容器命令
# -p	暴露端口，宿主机，容器内部端口。
[root@yanan /]# docker images
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
nginx        latest    d1a364dc548d   3 weeks ago    133MB	# 刚拉取下载的nginx
mysql        latest    c0cdc95609f1   5 weeks ago    556MB
centos       latest    300e315adb2f   6 months ago   209MB

# 进入容器
[root@yanan ~]# docker exec -it nginx01 /bin/bash
root@10e221d799fd:/# whereis nginx
nginx: /usr/sbin/nginx /usr/lib/nginx /etc/nginx /usr/share/nginx
root@10e221d799fd:/# cd /etc/nginx/
root@10e221d799fd:/etc/nginx# ls
conf.d	fastcgi_params	mime.types  modules  nginx.conf  scgi_params  uwsgi_params
# 这里就会有正常的nginx的配置.conf配置文件。
```

![image-20210621132859097](E:\Lklyx.github.io\source\_posts\Growth-Diary\扩展知识\Docker\image\2.png)

思考问题：我们每次改动nginx配置文件，都需要进入容器内部？十分麻烦，我要是可以在容器外部提供一个映射路径，达到在容器修改文件名，容器内部就可以自动修改？-v 数据卷！

> 作业:使用docker装一个tomcat。

```shell
# 官方使用
docker run -it --rm tomcat:9.0

# 我们之前的启动都是后台，停止了容器之后，容器还可以查到。docker run -it --rm 。这个是用来测试，用完就删除。

# 下载启动
docker pull tomcat

# 启动运行
docker run -d -p 3355:8080 --name tomcat01 tomcat
# 使用docker运行tomcat，在后台环境下，暴露一个3355:8080端口 运行，重命名为tomcat01

#进入容器 docer exec -it +容器名 /bin/bash
# 问题：测试访问没有问题，但是显示的是404页面。是因为docker全部简化了。这样的话webapps里面没有东西。
# 解决：我们复制webapps.dist里面的内容到webapps中，就可以正常显示tomcat页面了。
 cp -r webapps.dist/* webapps # 赋值 webapps.dist/*之下的所有目录，到webapps中。
```

思考问题：我们以后部署项目，如果每次都要进入容器是不是十分麻烦？我要是可以在容器外部提供一个映射路径，webapps，我们在外部放置项目，就自动同步到内部就好了。

> 作业：部署es + kibana

```shell
# es 暴露的端口很多！
# es 十分的耗内存
# es的数据一般需要防止到安全目录！挂载。

# 下载启动elasticsearch
# 加上es的配置。
docker run -d --name elasticsearch02 -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" -e ES_JAVA_OPTS="-Xms64m -Xmx512m" elasticsearch:7.6.2
# -e ES_JAVA_OPTS="-Xms64m -Xmx512m" -e 限制一些基本运行的函数 ES_java的环境，最小64m。最大运行给他512m

# 测试一下es是否成功
[root@yanan ~]# curl localhost:9200
{
  "name" : "901fb49e18c1",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "lP5Q8aoyS2COdm9WoEbqrg",
  "version" : {
    "number" : "7.6.2",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "ef48eb35cf30adf4db14086e8aabd07ef6fb113f",
    "build_date" : "2020-03-26T06:34:37.794943Z",
    "build_snapshot" : false,
    "lucene_version" : "8.4.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```

> 查看cpu使用率
>
> ```shell
> docker stats
> ```

## 可视化

- portainer（先用这个）

  ```shell
  docker run -d -p 8088:9000 \
  --restart=always -v/var/run/docker.sock:/var/run/docker.sock --privileged=true portainer/portainer
  ```

- Eancher（CI、CD再用）

**什么是Portainer？**

Docker 图形化界面管理工具！提供一个后台面板供我们操作！

```shell
docker run -d -p 8088:9000 \
--restart=always -v/var/run/docker.sock:/var/run/docker.sock --privileged=true portainer/portainer
# 这里需要去开通安全组的外网端口8088
```

访问测试。自己的ip加端口8088

通过他来访问了：

![image-20210623100939079](E:\Lklyx.github.io\source\_posts\Growth-Diary\扩展知识\Docker\image\3.png)

设置密码进入，我设置的为`admin123`

可视化面板我们平时不怎么使用，自己测试玩玩就可以了。

# Docker镜像讲解

## 镜像是什么？

18集、

## Docker镜像加载原理

19集、

## 分层理解

19集、

## commit镜像

docker commit 提交容器成为一个新的副本

```shell
# 命令和git原理类似
docker commit -m="提交的描述信息" -a="作者" 容器ID 目标镜像名:[Tag]
```

实战测试：

```shell
# 1、启动一个默认的tomat
# 2、发现这个默认的tomcat 是没有webapps应用，镜像的原因，官方的镜像默认 webapps下面是没有文件的！我们只好从webapps.dist文件中复制过去。这样就可以正常使用了。
# 3、我自己拷贝进去了基本的文件
# 4、将我们操作过的容器通过commit提交为一个镜像！我们以后就使用我们修改过的镜像即可，这就是我们自己的一个修改的镜像
```

![image-20210623132839144](E:\Lklyx.github.io\source\_posts\Growth-Diary\扩展知识\Docker\image\4.png)

到了这里，才算是docker入门！

# 容器数据卷

## 什么是容器数据卷

![image-20210623133945173](E:\Lklyx.github.io\source\_posts\Growth-Diary\扩展知识\Docker\image\5.png)

总结一句话：容器的持久和同步操作！容器间也是可以数据共享的！

## 使用数据卷

> 方式一：直接使用命令来挂载 -v

```shell
docker run -it -v
# -v 主机目录：容器内目录，做一个映射。

# 测试：
docker run -it -v /home/ceshi:/home centos /bin/bash
-it # 在里面去执行
-v # 挂载
/home/ceshi:/home # /home/ceshi是虚拟机上的测试目录。：跟容器里面的/home对应映射。
centos # 启动镜像

# 启动起来时候我们可以通过docker inspect + 容器ID  查看具体信息。
```

![](E:\Lklyx.github.io\source\_posts\Growth-Diary\扩展知识\Docker\image\6.png)

测试文件的同步

![image-20210623152819024](E:\Lklyx.github.io\source\_posts\Growth-Diary\扩展知识\Docker\image\7.png)

再来测试：

1. 停止容器，不是删除，是停止，exit。退出，停止。
2. 宿主机上修改文件
3. 启动容器
4. 容器内的数据依旧同步的

好处：我们以后修改只需要在本地修改即可，容器内会自动同步。

## 实战：安装MySQL

思考：MySQL的数据持久的问题

```shell
# 获取镜像
docker pull mysql:5.7
# 运行容器，需要做数据挂载! 
# 安装启动mysql，是需要配置密码的，这是需要注意的点。官网的是这样的。
docker run --name some-mysql -v /my/custom:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag

# 启动我们的mysql
docker run -d -p 3310:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name mysql01 mysql:5.7
-d 后台运行
-p 3310:3306	端口映射
-v /home/mysql/conf:/etc/mysql/conf.d	卷挂载，映射配置挂载
-v /home/mysql/data:/var/lib/mysql	卷挂载，映射数据挂载
-e MYSQL_ROOT_PASSWORD=123456	环境配置，配置mysql的密码。
--name mysql01 	容器的名字。
mysql:5.7 # 需要启动的名字加版本号

# 启动成功以后，我们在本地使用navcat来测试一下， 记得在服务器配置3310端口
# navcat -连接到服务的3310 --- 3310和容器内的 3306映射，这个是我们就可以连接上了！
# 在本地创建一个数据库，查看我们的映射是否ok！

```

## 具名挂载和匿名挂载

```shell
# 匿名挂载
-v 容器内路径！
docker run -d -P --name nginx01 -v /ect/nginx nginx

# 查看所有的volume
[root@yanan data]# docker volume ls
DRIVER    VOLUME NAME
local     0b8665fdb3d8541564c963d0d8ac06f3fc2443a9de1e2e94a5182ff886f6b22f
local     3d9a65b7398b9c809a02eff681a9ede7065225bf918c376ac91094ac92664f57
local     6e24a2ff87e1f4840d33e7427ee6b59b88c45d314e973f290146e43f625a7934
local     7c6011f63bb4cc96a3b725d17c8b363962748f703a7c4ce8827b9717dea9efda
local     8ca7d1ef73b3eeee67f8af2da4b9b6c43f989bda4837c8bfdf38fb55c8a0ab2f
local     9eee80503bf966349d4fefaa4b449942a81c252449fd0ad1471a30e43c20f454
local     58cf2baf4712c05dafc2b0a48aa8e36e12bc1e7e38fe41c9ea9d8ef16f478a11

# 具名挂载
# 通过-v 卷名：容器内路径
# 查看一下这个卷
local     bda56e90dc819b3bc9ba87e4c8ada55c05ba83c646e5f440b67adf32ff6c3d1c
local     dca55220d001343ea5ff1696176b9c18ebe5526c88f98cbbec21dbaed9376086
local     fe707bc573dfcb8cf1bc19553de1f09725c72ed11f1901038381f72503f660dd
local     juming-nginx
[root@yanan data]# docker volume inspect juming-nginx
[
    {
        "CreatedAt": "2021-06-24T13:16:54+08:00",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/juming-nginx/_data",
        "Name": "juming-nginx",
        "Options": null,
        "Scope": "local"
    }
]

```

所有的docker容器内的卷，没有指定目录的情况下，都是在`/var/lib/docker/volumes/xxx/data`

我们通过具名挂载可以方便的找到我们的一个卷，大多数情况都在使用的`具名挂载`

```shell
# 如何确定是具名挂载还是匿名挂载，还是指定路径挂载！
-v 容器内路径	# 匿名挂载
-v 卷名：容器内路径		# 具名挂载
-v /宿主机路径:容器内路径		# 指定路径挂载
```

拓展：

```shell
# 通过-v 容器内路径：ro rw 改变读写权限。
ro readonly # 只读
rw readwrite # 可读可写
# ro只要看到ro就说明这个路径只能通过宿主机来操作，容器内部是无法操作!
```

## 初识Dockerfile

Dockerfile就是用来构建docker镜像的构建文件！命令脚本！体验一下！

通过这个脚本可以生成镜像，镜像是一层一层的，脚本是一个个的命令，每个命令都是一层

```shell
# 创建一个dockerfile文件，名字可以随机 建议dockerfile
# 文件中的内容 指令（大写）参数
FROM centos
VOLUME ["volume01","volume02"]
CMD echo "---end----"
CMD /bin/bash
# 这里的每个命令，就是镜像的一层！
```

> 方式二：

![image-20210625145050645](E:\Lklyx.github.io\source\_posts\Growth-Diary\扩展知识\Docker\image\8.png)

```shell
# 启动自己写的容器

run start + 容器id
```

## Dockerfile体系结构

```shell
FROM	# 基础镜像，当前新镜像是基于那个镜像的
MAINTAINER	# 镜像维护者的姓名和邮箱地址
RUN		# 容器构建时需要运行的命令
EXPOSE 	 # 当前容器对外暴露的端口
WORKDIR 	# 指定在创建容器后，终端默认登录的工作目录。
ENV 	 # 用来在构建镜像过程中设置环境变量的
ADD 	# 将宿主机目录下的文件拷贝进镜像且ADD命令会自动处理URL和解压tar压缩包
COPY 	# 类似ADD，拷贝文件到镜像目录中。
VOLUME 	# 容器数据卷，用于数据保存和持久化工作
CMD 	#  指定一个容器启动时要运行的命令，Dockerfile可以有多个CMD指令，单只有最后一个生效，CMD会被docker run之后的参数替换
ENTRYPOINT # 指定一个容器启动时要运行的命令，
```

