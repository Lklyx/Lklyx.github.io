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

```js
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
