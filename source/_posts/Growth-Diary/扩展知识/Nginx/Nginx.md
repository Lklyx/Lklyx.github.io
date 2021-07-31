---
title: Nginx学习
date: 2021/05/31
categories:
- [历练ing,扩展知识,Nginx]
tags:
- Nginx
---

# 学习地址

Nginx官网[nginx](http://nginx.org/en/download.html)

学习视屏地址[Nginx](https://www.bilibili.com/video/BV1zJ411w7SV?p=2&spm_id_from=pageDriver)

学习视屏地址[Nginx](https://www.bilibili.com/video/BV1j4411K7g2?from=search&seid=11242539390432733612)

虚拟机安装视频[centOs](https://www.bilibili.com/video/BV15z4y197sk?t=1191)

# Nginx概述

Nginx（engine x）是一个高性能的HTTP和反向代理服务器，特点是占用内存少，并发能力强，事实上，Nginx的并发能力确实在同类型的网页服务器中表现较好，中国大陆使用nginx的网站用户有：百度、京东、新浪、网易、腾讯、淘宝等。

# 安装

> 1. 安装依赖项，使用以下命令安装Nginx需要的依赖项。
>
>    ```shell
>    yum -y install gcc zlib zlib-devel pcre-devel openssl openssl-devel
>    ```
>
>    安装好依赖项以后，使用以下命令查看版本号：
>
>    ```sh
>    pcre-config --version
>    ```
>
> 2. 解压拖进去的nginx安装包
>
>    ```shell
>    tar -xvf + apache-tomcat-9.0.46-fulldocs.tar.gz # + 后面这个是安装包名字。
>    ```
>
> 3. 解压好以后进入解压的文件夹执行：**./configure**，编译文件
>
>    ```shell
>    ./configure
>    ```
>
> 4. 使用**make && make install**
>
>    ```shell
>    make && make install
>    ```

安装成功之后，在usr中会多出来一个文件夹**/usr/nginx**,在nginx中，有sbin的启动脚本。

# 防火墙

1. 开启防火墙

   ```shell
   systemctl start firewalld
   ```

2. 关闭防火墙

   ```shell
   systemctl stop firewalld
   ```

3. 查看防火墙中开放的端口

   ```shell
   firewall-cmd --list-all
   ```

   后期需要在防火墙中添加端口号，使用以下命令：

   ```shell
   sudo firewall-cmd --add-port=8080/tcp --permanent  # 添加一个81端口
   ```

   添加成功以后，需要重启以下防火墙：

   ```shell
   firewall-cmd --reload # 重启防火墙
   ```

   这时候再去2、查看防火墙的端口，就会多了一个81端口。

# 实现上传压缩包rz

安装**lrzsz**

```js
yum -y install lrzsz
```

# 解压压缩包命令

```js
tar -xvf + apache-tomcat-9.0.46-fulldocs.tar.gz // + 后面这个是安装包名字。
```

# Linux中配置安装jdk及环境配置。

## 我们直接可以使用yum一键安装

```java
yum install -y java-1.8.0-openjdk-devel // 这里装完以后记得去配置jdk环境变量
```

查看java版本，

```java
java -version
```

## 配置环境变量

1. 找到java安装的路径

   ```js
   whereis java // 查看路径
   // /usr/bin/java /usr/lib/java /etc/java /usr/share/java /usr/share/man/man1/java.1.gz
   
    ls -lrt /usr/bin/java // 查看java的bin之下路径
   // /usr/bin/java -> /etc/alternatives/java
   
   ls -lrt /etc/alternatives/java // 查看需要配置环境的路径
    // /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.212.b04-0.el7_6.x86_64/jre/bin/java
   /usr/lib/jvm/jre-1.7.0-openjdk.x86_64/bin/java
   ```

2. 进入文件夹配置环境变量

   ```java
   vim /etc/profile // 进入java环境变量配置单的文件
   ```

   在文件的末尾处添加以下代码：

   ```java
   export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.292.b10-1.1.al7.x86_64
   export PATH=$JAVA_HOME/jre/bin:$PATH
   export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
   ```

   `注意：`上面代码的第一行，**export JAVA_HOME=**之后，改为你自己的路径，切注意，路径不包含版本号、系统号之后的`/jre/bin/java` 这个路径。

3. 使配置生效

   ```java
   source /etc/profile
   ```

4. 查看JAVA_HOME环境变量

   ```java
   echo $JAVA_HOME
   // /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.212.b04-0.el7_6.x86_64
   ```

# Nginx常用命令

`使用Nginx操作命令前提条件：`必须进入nginx目录中。

```shell
/usr/local/nginx/sbin
```

1. **nginx的版本号**

   ```shell
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

# Nginx配置实例——反向代理

1. 在dindows系统的host文件中进行域名和ip对应关系的配置

   一般的目录地址是：**c:Windows/System32/drivers/etc**，在里面加上一段ip。比如：106.15.176.231 www.123.com。前面是ip地址，后面是你的域名。

2. 在nginx进行请求转发的配置（反向代理配置）

   找到nginx的配置文件。一般在：**/usr/local/nginx/conf**这个路径之下。打开配置以下项；

   ![image-20210607134411528](E:\Lklyx.github.io\source\_posts\Growth-Diary\扩展知识\Nginx\Nginx\8.png)

   将server中的**server_name localhost**改为server_name + 自己的ip。

   在location中添加一个转发路径：

   ```shell
   proxy_pass http:127.0.0.1:8080
   ```

   这样做，如果我们访问的是自己的ip：**106.15.176.231**，如果他是80端口，他就会给我们转发到**127.0.0.1:8080**端口去。

## 根据不同的路径，跳转到不同的tomcat中

实现效果：

- 访问：http://127.0.0.1:9001/edu/ 直接跳到127.0.0.1:8080 端口去。
- 访问：http://127.0.0.1:9001/vod/ 直接跳到127.0.0.1:8081 端口去。

准备工作：

1. 准备两个tomcat服务器。

   在目录：**usr/src**下创建两个文件夹，分别为tomcat8080、tomcat8081。

   ```shell
   mkdir tomcat8080
   mkdir tomcat8081
   ```

   这是可以把之前的tomcat进程关闭。

   ```shell
   # 查看当前的tomcat进程
   ps -ef | grep tomcat
   # 关闭进程
   sill -9 + id # 这里是数字9，而不是字母G,ID.查看进程时前面的就是
   ```

   在两个文件里面分别放入tomcat的安装包、并解压、启动（**/usr/src/tomcat8081/apache-tomcat-7.0.70/bin**）之下，执行命令

   ```shell
   ./startup.sh 
   ```

   8080 和8081 文件夹中的tomcat都启动以后，8080默认的端口号就是8080，所以不用我们修改。我们需要进入8081文件夹中，修改它的配置文件。路径为：**/usr/src/tomcat8081/apache-tomcat-7.0.70/conf** 之中的`server.xml`文件。

   ```cmd
   vi server.xml
   ```

   ![image-20210607172045416](E:\Lklyx.github.io\source\_posts\Growth-Diary\扩展知识\Nginx\Nginx\9.png)

   Server port 改为8015，

   ![image-20210607172207668](E:\Lklyx.github.io\source\_posts\Growth-Diary\扩展知识\Nginx\Nginx\10.png)

   主要的connector port改为8081。

   改成功以后分别启动8080和8081。这时，我们启动了两个tomcat。可以直接去地址栏输入地址。

2. 创建文件夹和测试页面。

   因为我们创建的页面是在`webapps`中，所以我们进到这个目录中去，给他分别建立两个文件夹。**edu、ovd。**在这两个文件夹中，分别放入不同的**html**文件就可以了。这时，我们可以在浏览器输入ip地址，试试不同的端口看效果。

具体配置：

1. 找到nginx配置文件，进行反向代理配置。

   ![image-20210607175034486](E:\Lklyx.github.io\source\_posts\Growth-Diary\扩展知识\Nginx\Nginx\11.png)

2. 开放对外访问的端口号：9001、8080、8081、

# Nginx配置实例——负载均衡。

实现效果：

在浏览器地址栏输入地址：http://106.15.176.231，负载均衡效果，平均分配到8080和8081端口中。

准备工作	

- 准备两台tomact服务器，一台8080，一台8081.
- 在两台tomcat里面webapps目录中。创建名称是edu的文件夹，在文件夹中创建页面**a.html**，用于测试

在nginx的配置文件中进行负载均衡的配置

- 进入nginx的配置中去，在http中配置
- ![image-20210608114542443](E:\Lklyx.github.io\source\_posts\Growth-Diary\扩展知识\Nginx\Nginx\12.png)

在**http**块中，加一个==upstreat myserver==后面的**myserver**是名字，可以自定义。在新加块中加上我们的服务器列表。

```shell
upstreat myserver{
	server 106.15.176.231:8080
	server 106.15.176.231:8081
}
```

在**http==>server**之中，修改`server_name` 的值为自己的ip地址。然后在之下的`location`中，使用proxy_pass  http:// + 上面自定义的名字。实现效果。

```cmd
location / {
	proxy_pass  http://myserver  #这里的myserver是自定义名字。
}
```

## nginx负载均衡的策略

1. **轮询**（默认）

   每个请求按时间顺序逐一分配到不同的后端服务器，如果某后端服务器停止了。能自动剔除。

2. **weight权重**

   weight代表权重，默认为1.权重越高被分配的客户端越多。指定轮询几率，weight和访问比率成正比，用于后端服务器性能不均的情况。例：

   ```shell
   upstreat myserver{
   	server 106.15.176.231:8080  weight=5;
   	server 106.15.176.231:8081  weight=10;
   }
   ```

   以上代码的8080端口的权重低于8081，这时8081端口的客户端量就会比8080多一倍。

3. **ip_hash**

   ```shell
   upstreat myserver{
   ip_hash;  #加上这句话就是ip_hash
   	server 106.15.176.231:8080;
   	server 106.15.176.231:8081;
   }
   ```

   意思是。当你第一次访问的是8080，他就默认记住你的这个ip访问的就是8080，以后你的每次访问都会是8080。这种方法可以解决session的问题。

4. **fair**

   按后端服务器的响应时间来分配请求，响应时间短的优先分配。

   ```shell
   upstreat myserver{
   	server 106.15.176.231:8080;
   	server 106.15.176.231:8081;
   	fair;  #加上这句话就是fair策略
   }
   ```

   解：同时发起访问请求。这是会默认有8080、8081接到请求。但是，谁先接受到。就是谁访问。就是看当前的服务器那个端口响应的时间短了。



# Nginx配置实例——动静分离。（测试失败！）

1. 什么是动静分离；

   Nginx动静分离简单来说就是把动态跟静态请求分开,不能理解成只是单纯的把动态页面和静态页面物理分离。严格意义上说应该是动态请求跟静态请求分开，可以理解成使用Neinx处理静态页面，Tomcat处理动态页面。动静分离从目前实现角度来讲大致分为两种，
   一种是纯粹把静态文件独立成单独的域名,放在独立的服务器上，也是目前主流推崇的方案;另外一种方法就是动态跟静态文件混合在一起发布，通过nginx来分开。通过 location 指定不同的后缀名实现不同的请求转发。通过 expires参数设置，可以使浏览器缓存过期时间，减少与服务器之前的请求和流量。具体Expires定义:是给一个资源设定一个过期时间,也就是说无需去服务端验证,直接通过浏览器自身确认是否过期即可，所以不会产生额外的流量。此种方法非常适合不经常变动的资源。(如果经常更新的文件，不建议使用 Expires来缓存），我这里设置3d，表示在这3天之内访问这个URL，发送一个请求，比对服务器该文件最后更新时间没有变化，则不会从服务器抓取，返回状态码304，如果有修改，则直接从服务器重新下载，返回状态码200。

2. 准备工作；

   在linux系统中准备静态资源，用于进行访问，在跟目录下创建一个名为**data**的文件夹，并在data中创建两个子文件夹。www和image、分别存放动态资源和静态资源。

3. 具体配置；

   - 在nginx配置文件中进行配置

     ![image-20210610133516870](E:\Lklyx.github.io\source\_posts\Growth-Diary\扩展知识\Nginx\Nginx\13.png)

     配置中：autoindex on是为了把文件以列表的形势排列出来。

# Nginx配置高可用集群

学习视频[高可用集群](https://www.bilibili.com/video/BV1zJ411w7SV?p=14&spm_id_from=pageDriver)

1. 高可用集群

   - 什么是高可用？

     高可用HA（High Availability）是分布式系统架构设计中必须考虑的因素之一，它通常是指，通过设计减少系统不能提供服务的时间。如果一个系统能够一直提供服务，那么这个可用性则是百分之百，但是天有不测风云。所以我们只能尽可能的去减少服务的故障。

   - 解决的问题？

     在生产环境上很多时候是以`Nginx`做反向代理对外提供服务，但是一天Nginx难免遇见故障，如：服务器宕机。当`Nginx`宕机那么所有对外提供的接口都将导致无法访问。

   - 双机热备份？

     这种方案是国内企业中最为普遍的一种高可用方案，双机热备其实就是指一台服务器在提供服务，另一台为某服务的备用状态，当一台服务器不可用另外一台就会顶替上去。

2. 配置高可用的准备工作

   - 需要两台服务器
   - 在两台服务器上都安装nginx
   - 在两台服务器上都安装keepalived

3. 在两台服务器上安装keepalived

   使用yum命令安装

   ```shell
   yum install keepalived -y
   ```

   安装好以后，使用：rpm -q -a keepalived 这个命令查看安装的版本号。

   ```shell
   rpm -q -a keepalived
   ```

   keepalived的安装位置在：

   ```shell
   cd /etc // 安装位置
   cd keepalievd/  // 进入目录
   vi keepalievd.conf // 进入配置文件
   ```

4. 完成高可用配置（主从配置）

   1. **修改主机（192.168.16.128）keepalived配置文件**

      ```shell
      #检测脚本
      vrrp_script chk_http_port {
          script "/usr/local/src/nginx_check.sh" #心跳执行的脚本，检测nginx是否启动
          interval 2                          #（检测脚本执行的间隔，单位是秒）
          weight 2                            #权重
      }
      #vrrp 实例定义部分
      vrrp_instance VI_1 {
          state MASTER            # 指定keepalived的角色，MASTER为主，BACKUP为备
          interface ens33         # 当前进行vrrp通讯的网络接口卡(当前centos的网卡) 用ifconfig查看你具体的网卡
          virtual_router_id 66    # 虚拟路由编号，主从要一直
          priority 100            # 优先级，数值越大，获取处理请求的优先级越高
          advert_int 1            # 检查间隔，默认为1s(vrrp组播周期秒数)
          #授权访问
          authentication {
              auth_type PASS #设置验证类型和密码，MASTER和BACKUP必须使用相同的密码才能正常通信
              auth_pass 1111
          }
          track_script {
              chk_http_port            #（调用检测脚本）
          }
          virtual_ipaddress {
              192.168.16.130            # 定义虚拟ip(VIP)，可多设，每行一个
          }
      }
      ```

      `virtual_ipaddress` 里面可以配置vip,在线上通过vip来访问服务。

      `interface``需要根据服务器网卡进行设置通常查看方式``ip addr`

      `authentication`配置授权访问后备机也需要相同配置

   2. **修改备机（192.168.16.129）keepalived配置文件**

      ```shell
      #检测脚本
      vrrp_script chk_http_port {
          script "/usr/local/src/nginx_check.sh" #心跳执行的脚本，检测nginx是否启动
          interval 2                          #（检测脚本执行的间隔）
          weight 2                            #权重
      }
      #vrrp 实例定义部分
      vrrp_instance VI_1 {
          state BACKUP                        # 指定keepalived的角色，MASTER为主，BACKUP为备
          interface ens33                      # 当前进行vrrp通讯的网络接口卡(当前centos的网卡) 用ifconfig查看你具体的网卡
          virtual_router_id 66                # 虚拟路由编号，主从要一直
          priority 99                         # 优先级，数值越大，获取处理请求的优先级越高
          advert_int 1                        # 检查间隔，默认为1s(vrrp组播周期秒数)
          #授权访问
          authentication {
              auth_type PASS #设置验证类型和密码，MASTER和BACKUP必须使用相同的密码才能正常通信
              auth_pass 1111
          }
          track_script {
              chk_http_port                   #（调用检测脚本）
          }
          virtual_ipaddress {
              192.168.16.130                   # 定义虚拟ip(VIP)，可多设，每行一个
          }
      }
      ```

   3. **检测脚本：**

      ```shell
      #!/bin/bash
      #检测nginx是否启动了
      A=`ps -C nginx --no-header |wc -l`        
      if [ $A -eq 0 ];then    #如果nginx没有启动就启动nginx                        
            systemctl start nginx                #重启nginx
            if [ `ps -C nginx --no-header |wc -l` -eq 0 ];then    #nginx重启失败，则停掉keepalived服务，进行VIP转移
                    killall keepalived                    
            fi
      fi
      ```
   
5. 分别启动两台服务器的nginx和keepalived。

   ```shell
   service keepalived restart	#启动keepalived 虚拟机
   systemctl start keepalived.service #启动keepalived 服务器
   ```

# 安装SSL证书+部署

1. 进入申请域名证书的网址，在里面输入想申请证书的域名，一定不要输入错误。

   https://freessl.cn/

2. 安装**KeyManager**并且打开他。

3. 进去登录，照着步骤走就是了。

   - 这里要求域名注测成功
   - 域名已经实名认证
   - 添加一条**KeyManage**给的解析值，解析类型为TXT。解析值为KeyManage给的值，华为云的添加解析记录需要加上英文状态下的双引号。

4. 添加解析值以后，下一步，检测配置。检测成功以后，会自动打包证书的。这时候下载保存。

5. 开始按照华为云的安装证书步骤一步一步的走

   https://support.huaweicloud.com/usermanual-scm/scm_01_0082.html#scm_01_0082__zh-cn_topic_0000001124217601_scm_01_0082_table4462648181517

   - 第一步

     先搞清楚是系统生成的，还是自己手动生成的。一般都是系统生成的。

     这时候你可以查看解压的文件夹中的Nginx文件夹。我用的是直接打开**KeyManage**，域名后面的三个小点，点开，直接查看PEM。往下滑，就会看到证书链和私钥了。（私钥用的是PKCS1的）。点击一键部署，一般不成功。还是得自己写配置。

   - 第二步

     创建一个名字为`cret`的文件夹，这个文件夹里面创建两个文件分别是：`server.crt`和`server.key`。其中，**server.crt**中保存的是证书和证书链，**server**中保存的是私钥。==注意==这里的cret这个文件夹，必须放在nginx配置文件的nginx.conf同路径下。因为下面配置路径的时候，不能写根路径。

   - 第三部

     修改配置文件，详情见7.

   - 第四步

     检验，配置是否正确。在**/usr/local/nginx**目录下输入：

     ~~~shell
     sbin/nginx -t
     ~~~

     如果显示以下类容，证明配置成功

     ~~~shell
     nginx.conf syntax is ok
     nginx.conf test is successful
     ~~~

     但是这里经常不成功。有可能是nginx没有打开ssl配置。这时候需要重新配置nginx。方法如下。到时候再百度搜索这种报错，解决方案都一样。

6. 进入Nginx中进行配置。进入nginx的目录。`/usr/local/nginx/conf/nginx.conf`

7. 配置如下：

   ~~~shell
   #user  nobody;
   worker_processes  1;
   
   events {
       worker_connections  1024;
   }
   
   http {
       include       mime.types;
       default_type  application/octet-stream;
   
       #  log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
       #                  '$status $body_bytes_sent "$http_referer" '
       #                  '"$http_user_agent" "$http_x_forwarded_for"';
   
       #access_log  logs/access.log  main;
   
       sendfile        on;
       # tcp_nopush     on;
   
       # keepalive_timeout  0;
       keepalive_timeout  65;
   
       server {
          listen       80;
   #       server_name  123.60.51.170;
          server_name  www.xn--xkr52xh3grqg.cn;
          return 301 https://$server_name$request_uri;
          # rewrite ^(.*)$  https://$host$1 permanent; 
          # access_log  logs/host.access.log  main;
   
           location / {
              root   html;
              index  index.html index.htm;
           }
           # 这是做动静分离加的测试页面。在data之下;
           location /www/ {
   	root   /data/;
               index  index.html index.htm;
           }
   
           # 这是做动静分离添加的图片路径;
   	location /image/ {
                  root   /data/;
                  autoindex   on;
             }
        }
   
   
       # another virtual host using mix of IP-, name-, and port-based configuration
   
       # HTTPS server
       
       server {
           listen		443 ssl;
           # listen		123.60.51.170:9001;
   
           server_name  www.xn--xkr52xh3grqg.cn;
   #        rewrite ^(.*)$  https://$host$1 permanent; 
   #        rewrite ^/(.*)$  http://www.xn--xkr52xh3grqg.cn/$1 permanent; 
   
           ssl_certificate     cert/_server.crt;	
           ssl_certificate_key  cert/_server.key;
   
           ssl_session_cache    shared:SSL:1m;
           ssl_session_timeout  5m;
   
           ssl_ciphers  HIGH:!aNULL:!MD5;
           ssl_prefer_server_ciphers  on;
   
           location / {
               root   html;
               index  index.html index.htm;
           }
       }
   
   }
   ~~~

8. 网站配置好以后，重启nginx服务器。如果显示重定向次数过多。这有可能是配置中，同时使用配置了多个server模块。网上搜索301报错。可以解决。

# 开启Nginx的SSL模块

1. Nginx如果未开启SSl模块，配置`https`时会提示错误。

   原因很简单：nginx缺少http_ssl_module模块，编译安装的时候带上--with-http_ssl_module配置就行了。

2. Nginx开启SSL模块

   切换到源码包：也就是自己的安装包所在的路径位置。

   ```sh
   cd /usr/src/nginx-1.14.2
   ```

   查看nginx原来模块

   ```sh
   /usr/local/nginx/sbin/nginx -V
   ```

   在configure arguments:后面显示的原有的configure参数如下：

   ```shell
   --prefix=/usr/local/nginx --with-http_stub_status_module
   ```

   这个就是装好，有SSL模块的。

3. 新配置

   在我们的源码包路径下这样配置：

   ```shell
   ./configure --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_ssl_module
   ```

4. 配好了上面的配置以后，

   ```shell
   make
   ```

   `注意`：这里不能配置 ==make install==。否者就是覆盖安装了。

5. 备份原来安装好的nginx

   这个是在哪里敲命令都可以，毕竟是复制嘛，只要写清楚复制什么的路径，复制到哪里，就可以了。

   ```shell
   cp /usr/local/nginx/sbin/nginx /usr/local/nginx/sbin/nginx.bak
   ```

   这nginx安装的路径下，复制一个同路径的文件 来作为备份。

6. 停止nginx。

   ```shell
   ./nginx
   kill ./nginx
   ```

7. 复制刚编译好的nginx，覆盖原来的nginx。

   刚编译好的，就是在我们安装包路径下的`./objs/nginx`文件中。

   原来的就在原来安装的位置。`/usr/local/nginx/sbin/`

8. 启动nginx。通过命令查看是否加入SSL模块成功

   ```shell
   /usr/local/nginx/sbin/nginx -V　
   ```

   