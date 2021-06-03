---
title: Nginx学习
date: 2021/05/31
categories:
- [历练ing,扩展知识,Nginx]
tags:
- Nginx
---

# 学习地址

学习视屏地址[Nginx](https://www.bilibili.com/video/BV1zJ411w7SV?p=2&spm_id_from=pageDriver)

学习视屏地址[Nginx](https://www.bilibili.com/video/BV1j4411K7g2?from=search&seid=11242539390432733612)

# Nginx概述

Nginx（engine x）是一个高性能的HTTP和反向代理服务器，特点是占用内存少，并发能力强，事实上，Nginx的并发能力确实在同类型的网页服务器中表现较好，中国大陆使用nginx的网站用户有：百度、京东、新浪、网易、腾讯、淘宝等。

# 安装

> 1. 安装依赖项，使用以下命令安装Nginx需要的依赖项。
>
>    ```js
>    yum -y install gcc zlib zlib-devel pcre-devel openssl openssl-devel
>    ```
>
>    安装好依赖项以后，使用以下命令查看版本号：
>
>    ```js
>    pcre-config --version
>    ```
>
> 2. 开启防火墙
>
>    ```js
>    systemctl start firewalld
>    ```
>
>    
>
> 3. 查看防火墙中开放的端口
>
>    ```js
>    firewall-cmd --list-all
>    ```
>
>    后期需要在防火墙中添加端口号，使用以下命令：
>
>    ```js
>    sudo firewall-cmd --add-port=81/tcp --permanent  // 添加一个81端口
>    ```
>
>    添加成功以后，需要重启以下防火墙：
>
>    ```js
>    firewall-cmd --reload // 重启防火墙
>    ```
>
>    这时候再去2、查看防火墙的端口，就会多了一个81端口。

# Nginx常用命令

`使用Nginx操作命令前提条件：`必须进入nginx目录中。

```js
/usr/local/nginx/sbin
```

1. **nginx的版本号**

   ```js
   ./nginx -v
   ```

2. **启动nginx**

   ```js
   ./nginx
   ```

3. **关闭nginx**

   ```js
   ./nginx -s stop
   ```

4. **重新加载nginx**

   ```js
   ./nginx -s reload
   ```

# nginx配置文件

1. 配置文件的位置：

   ```js
   ./usr/local/nginx/conf/nginx.conf
   ```

   ![配置文件的位置](E:\Lklyx.github.io\source\_posts\Growth-Diary\扩展知识\Nginx\Nginx\image-20210602171842698.png)

2. nginx配置文件的组成

   - nginx配置文件有三部分组成

     **第一部分** 全局块

     ![image-20210602173316902](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210602173316902.png)

     从配置文件开始到events块之间的内容，主要会设置一些影响nginx服务器整体运行的配置指令。

     比如：worker_processes ,worker_processes值越大，可以支持的并发处理量也越多。

     **第二部分** events块

     ![image-20210602173637443](E:\Lklyx.github.io\source\_posts\Growth-Diary\扩展知识\Nginx\Nginx\image-20210602173637443.png)

     events块涉及的指令主要影响Nginx服务器与用户的网络连接。

     比如：worker_connections 1024;

     **第三部分** http块

     Nginx服务器中，配置最频繁的部分，http块也可以包括http全局块、server块

# 解压压缩包命令

```js
tar -xvf + apache-tomcat-9.0.46-fulldocs.tar.gz // + 后面这个是安装包名字。
```

# 配置安装jdk及环境配置。

我们直接可以使用yum一键安装

```java
yum install -y java-1.8.0-openjdk-devel.x86_64
```

查看java版本，

```java
java -version
```

