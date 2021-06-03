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
