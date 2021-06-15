---
title: Nginx踩坑篇
date: 2021/05/31
categories:
- [历练ing,扩展知识,Nginx]
tags:
- Nginx
---

# Xshell

学习Nginx需要装`Xshell`这个工具。装这个连接远程，方便操作。

安装地址为：https://pan.baidu.com/s/1NGTD4VNSbl0bWCT7zJ0klA

提取码：7b8j

下载这个软件压缩包，里面有文档指导安装破解版的。

# 实现拖拽上传下载文件的解决方法

安装**lrzsz**，

```cmd
yum -y install lrzsz
```

使用方法：这时候可以直接敲命令rz、sz、下载和上传数据了。

上传文件：rz + 文件名

下载文件：sz + 文件名

如果报错，显示传输失败，有可能是名字相同了。或者改文件夹下这个名字已经存在该文件了。这时，我们只需要修改一下文件的名字即可。

# 配置好防火墙了，端口也设置了80.就是进不去nginx。

我靠。这个问题我搞了一天。原来是因为服务器没有配置安全组。我的是阿里云服务器，需要配置安全组。![image-20210603154118108](E:\Lklyx.github.io\source\_posts\Growth-Diary\扩展知识\Nginx\Nginx\image-20210603154118108.png)

感觉这个巨坑了。有的服务器不需要手动配置安全组。

# 阿里服务器需要配置安全组

![image-20210607115621226](E:\Lklyx.github.io\source\_posts\Growth-Diary\扩展知识\Nginx\Nginx\image-20210607115621226.png)

# make: *** No targets specified and no makefile found. Stop.

第一种：

第一、update最新版本系统软件

yum update

这个必须要执行后才可以安装我们的系统软件或者一键包。

第二、编译缺失关联软件

yum install gcc build-essential

编译执行完毕之后，我们在执行./configure && make这类的执行命令就可以解决问题。


第二种：

一、Linux下各种依赖都已经安装,是因为没有找到makefile。

如果是自己写的，确定在当前目录下；如果是源码安装，先运行./configure，生成makefile，再执行make，即可正常运行。

二、如果没有安装其他依赖先安装依赖

yum install gcc gcc-c++ autoconf automake

yum -y install zlib zlib-devel openssl openssl-devel pcre pcre-devel （安装依赖zlib、openssl和pcre

# 在centOs虚拟机中无法使用yum命令

敲yum命令时，出现以下错误：

```cmd
[root@Linux1 home]# yum -y install gcc zlib zlib-devel pcre-devel openssl openssl-devel
Loaded plugins: fastestmirror, refresh-packagekit, security
Loading mirror speeds from cached hostfile
YumRepo Error: All mirror URLs are not using ftp, http[s] or file.
 Eg. Invalid release/repo/arch combination/
removing mirrorlist with no valid mirrors: /var/cache/yum/x86_64/6/base/mirrorlist.txt
Error: Cannot find a valid baseurl for repo: base
```

首先，这里说一下具体的原因：

> 1. CentOS 6已经随着2020年11月的结束进入了EOL（Reaches End of Life），不过有一些老设备依然需要支持，CentOS官方也给这些还不想把CentOS6扔进垃圾堆的用户保留了最后一个版本的镜像，只是这个镜像不会再有更新了
> 2. 官方便在12月2日正式将CentOS 6相关的软件源移出了官方源，随之而来逐级镜像也会陆续将其删除。
> 3. 不过有一些老设备依然需要维持在当前系统，CentOS官方也给这些还不想把CentOS6扔进垃圾堆的用户保留了各个版本软件源的镜像，只是这个软件源不会再有更新了。

`简单的说就是`：Centos 6已经不被官方支持，所以想要使用就要用其他代理比如阿里云Vault镜像。我下面使用的是阿里云的镜像。第三条命令可以看出来。

解决方案：

> ```cmd
>sed -i "s|enabled=1|enabled=0|g" /etc/yum/pluginconf.d/fastestmirror.conf
> ```
> 
> ```cmd
>mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
> ```
> 
> ```cmd
>curl -o /etc/yum.repos.d/CentOS-Base.repo https://www.xmpan.com/Centos-6-Vault-Aliyun.repo
> ```
> 
> ```cmd
>yum clean all
> ```
> 
> ```cmd
>yum makecache
> ```
> 
> 以上五条命令，按照顺序依次敲进去就可以了 。

# Another app is currently holding the yum lock; waiting for it to exit...

使用yum时出现这样的错误、且一直循环报错。

```cmd
vim /etc/yum.repos.d/CentOS-Base.repo # 进去修改enabled = 1
```

```cmd
rm -f /var/run/yum.pid #永久禁止该错误
```

然后就可以重新执行yum了。

# -bash: systemctl: command not found

开启防火墙，关闭防火墙。在虚拟机中打开防火墙。如果是服务器，记得在安全组中配置需要访问的端口。
