---
title: 学习Linux
date: 2021/05/19
categories:
- [历练ing,扩展知识,Linux]
tags:
- Linux
---

# 常用命令

```shell
 # 查看所有端口
netstat -tulnp
```

# Linux

学习视频地址[LINUX](https://www.bilibili.com/video/BV1pE411C7ho?p=1&spm_id_from=pageDriver)

[尚硅谷教学视频](http: //www.atguigu.com/download.shtml#linux)

安装下载位置，[Linux](https://www.jianshu.com/p/552179808ebf)

安装好以后去安装UBUNTU

# linux文件系统

linux中没有盘符的概念，只有一个根目录。根目录用`/`表示。

![image-20210528135454791](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210528135454791.png)

1. `/`根目录下有以下几个文件。

   - `/bin`
   - `/etc`
   - `/home`
   - `/lib`
   - `/usr`

   这些不同的目录都有不同的作用。每个目录的作用介绍可查看[Linux目录介绍](http://www.cnblogs.com/duanji/p/yueding2.html)

2. ## Linux常用命令

   - **pwd**查看当前在那个目录以及是那个用户。当前路径。

   - **ls**查看当前目录下有那些文件夹，有颜色的或者有后缀名的是文件夹，可以打开，没有的是文件。

   - **cd**进入到文件夹。进去了之后可以用`pwd`查看，使用cd可以打开多级路径，用/隔开，表示子目录。==注意：==区分大小写

     1. cd快捷键，我们可以使用`cd ..`进入目录，cd目录之下有些很长的文件夹名字，我们可能记不住，用ls查看很长也不想敲。这时候可以使用**Tab**键，快捷键打出来。点一下是直接获取到输入的首字母的文件，两下是打开以你输入的字母开头的文件。

     2. 回到家目录。直接

        ```java
        cd ~
        ```

        

   - **clear**，清空屏幕命令。

   - **ls -l**:罗列出目录，是以竖排这样的方式展示的，ls后面也可以跟路径，此时，罗列出来的目录就是该路径下的目录。

   - **ls -a**:罗列出影藏的文件目录。可以和**ls -l**一起使用。

     `**ls -l -a**`：竖排查看所有文件，包含隐藏文件。

     `**ls -lha**`：竖排显示所有文件，包含隐藏文件，且大小以`k`单位显示出来

     只要是隐藏的文件或隐藏的文件夹。用ls查看到的都是前面带个小点的。

     在Ubuntu中，如果想创建一个隐藏的文件或者文件夹，只需要在前面加一个点。

     **通配符**：类似正则表达式。

     - `*`：表示一个或多个。
     - `？`：一个字符。
     - [1、2、3]，也是代表一个字符，但是只能从中括号中选择一个字符。
     - [a-z]，是代表a到z中的任意一个字符。
     
   - **mv**：移动文件夹或文件，也就是剪切。如下：

     ```
     mv ceshi.txt /home/siki/weiwei
     mv hello2.txt /home/siki/Desktop/aa/127.txt 	//移动以后改名字为127.txt
     ```

     将`ceshi.txt`文件移动到`/home/siki/weiwei`文件夹之下。我们不但可以移动，还可以在移动的时候给他修改文件名字。也就是重命名。例：

     ```js
     mv test demo	//在当前文件夹中，移动test文件，且更换名字到当前文件夹。就是修改名字。
     ```

   - **cp**：复制文件夹或文件，和移动类似。复制是不删除原来位置的文件。复制的过程中，也可以重新命名。==注意：==**cp**复制时如果是文件夹需要在前面加上 `-r`。

   - **find**：精确搜索，

     ```apl
     find /home -name test.txt
     ```
     
     上面代码说明，在**home**路径下搜索名字为**test**的文件，只要是home下的任何子目录下的test文件都看搜索出来，搜索结果为：展示搜索文件的路径。
     
     ```js
     find /home -name he* 	// 名字中含有he的文件
     find /home -name '12*'  // 名字以12开头的文件
     find /home -iname 'abd'		//	名字为abc开头且不区分大小写。
     ```
     
     搜索**home**之下所有目录中，**名字**带有**he**的所有文件及文件夹。
     
     ```js
     locate 123  // 搜索索引库中的带有123的文件或者文件夹或者路径带有123的都索引出来。
     ```
     
   - **last**：查看出远程登录记录，其中包括，远程登录的账号、IP、星期、日期、时间、操作时长。

   - **echo $HISTSIZE**：用这个命令可以查看linux最多可以保存多少行记录。

   - **history|more**：这个命令可以查看所有的操作记录。使用空格翻页、一页一页的查看。

   - **history**：查询最近的历史操作记录

   - **top**：top命令经常用来监控linux的系统状况。能够实时显示系统中各个进程的资源占用情况。

3. 查看帮助手册，`需要查看帮助的命令`+`–-help`，`man`+需要查看的命令：如下

   ```
   ls --help
   mv --help
   
   man ls
   man mv  	//man命令使用q退出来。
   ```

4. **cat**：查看文件内容。所有内容直接打印出来，适用于查看内容少的文件。

   ```js
   cat -b 123.txt // 查看文件123.txt的内容，使用-b，是显示行号。此行号不包含空行。
   cat -n 123.txt // 查看文件123.txt的内容，使用-n，是显示行号。此行行包括空行。
   ```

   

5. **moar**：也是查看文件内容。所有内容直接打印出来，适用于查看内容少的文件。这个会打印换行。其他的与cat相似。

6. **grep**：抓取文件中的内容；

   ```java
   grpe user 123.txt // 搜索文件名为123.txt中，包含user字段的哪一行内容。
   grep -n user 123.txt // 加上一个-n，是为了显示搜索到的内容显示行号。空行也算行号的
   grpe -v user 123.txt // 反向搜索，搜索文件名为123.txt中，不包含user字段的哪一行内容。
   grpe ^'#' /etc/services // 抓取在/etc/services文件 中以#开头的数据。
   grpe s$ /home // 在/home中 以s结尾的 。
   grpe -i abc 123.txt // 在123.txt中查找abc。且忽略大小写。
   ```

7. **>** 和 **>>** ：**>**把得到或者查询出来的内容保存在其他文件夹，一个**>**代表是全部替换。两个**>>**代表是接在后面。比如：

   ```java
   grep siki 123.txt > test.txt // 抓取文件123.txt中，带有siki字段的内容 且 将它们保存或替换test.txt文件中的内容。如果没有test.txt文件。则会在当前目录下新创建一个test.txt文件用于保存抓取到的文件。
   grep siki 123.txt >> text.txt // 类似上面，唯一不懂的是，这个不是替换text.txt中的类容，而是将它接在text.txt文件内容的后面。
       // 例子如下：
   ll > 123.txt // ll以列表的形式查看当前目录。且把查看到的目录替换保存到123.txt中
   ll >> 123.txt // ll以列表的形式查看当前目录。且把查看到的目录保存到123.txt中
   ```

   总结：一个`>`替换。两个`>>`加在后面。有`text.txt`文件。替换里面的内容，若没有，创建新的`test.txt`文件。

8. **|**：管道。相当于做一个命令的连接。将一个命令的输出改变为输入。

9. **ln**：软连接。相当于windows的桌面快捷方式。

   ```java
   ln aa/123.txt aa_softlink // 意思是 为aa/123.txt 创建一个快捷方式，快捷方式的名字叫aa_softlin
   ```

   修改快捷方式里面的内容，原文件中的内容也会同时被修改。

# 用户管理、权限。

1.  添加用户：**sudo**

   `useradd`：添加新用户。

   `passwd`：添加密码。

   初始用户可以使用**sudo**添加新用户。

   ```java
   sudo useradd user1 // 前面的是命令，user1是需要添加的用户名。
   ```

   此处添加需要输入当前除使用户的登录密码作为验证。验证成功后，就可以创建成功了。我们用这个命令查看刚才创建的用户。

   ```java
   cat /etc/passwd	// 查看服务器所有用户。
   ```

   查看到已经创建的用户以后，给创建的用户设置登录密码

   ```java
   sudo passwd user1 // 使用命令sudo + 密码 + 需要设置密码的用户名。这里需要重复一遍
   ```

   ![查看创建的用户](E:\Lklyx.github.io\source\images\扩展知识\Linux\image-20210527102243369.png)

2. 给root设置密码：

   ```java
   sudo passwd root // root账户就是主账户，名字一般都是root。
   ```

   给root设置密码的时候需要验证一下当前账户的密码。

3. **切换用户**：**su**

   ```js
   su root // 使用su + 需要切换的用户的名字
   ```

   切换成功以后输入密码登录。

4. **退出root**：

   ```js
   exit // 退出root以后，会自动回到初始账号上面去
   ```

5. 删除用户：**userdel**

   ```js
   userdel user1 // 删除用户名为user1的用户。不删除家目录/home。
   userdel -r user1 // 加上-r这参数，就删除用户的家目录/home。
   ```

6. 用户组。

   - 添加用户组：**groupadd**

     ```js
     groupadd group1 // 添加一个组名为group1的用户组
     ```

     使用`cat /etc/group`查看是否添加成功。

     ```js
     cat /etc/group // 查看是否添加成功。
     ```

   - 修改用户组：**groupmod**

     ```js
     groupmod -n group1_new gronp // 需要加一个-n参数。这里注意先写需要改的名字，后面才写改的是哪个组。
     ```

   - 用户组的删除：**groupdel**

     ```js
     groupdel group1 // 直接删除命令加需要删除的组的名字。
     ```

   - 配置文件：**passwd**

     ```
     cat /etc/passwd // 操作系统下的配置文件。配置用户的配置。
     ```

7. 文件的权限

   - <img src="../../../../images/扩展知识/Linux/image-20210527173252136.png" alt="image-20210527173252136"  />

   - 使用`ll`命令查询出来之后，文件前面总是用很多`-`。前面的第一个是d，代表是文件夹，可以打开。第一个是`-`代表是文件。后面的9个`-`。前三个代表的是自己可以操作的权限。中间三个代表的是组**group**可以操作的权限。最后一个代表其他人可以操作的权限。

   - 其中：R W X 对应的是可读（read）、可写（write）、可执行（excute）。

   - 修改权限：**chmod**

     1. u：代表当前使用的用户。第123个`-`

     2. g：代表该用户所在的组。第456个`-`

     3. o：代表其他用户的权限。第789个`-`

     4. a：代表 **u、g、o**全部修改。

        **小结:**每个**u、g、o**中。又有**r、w、x**对应的读、写、执行权限

     ```js
     chmod u+x // 这个意思是，使用修改权限的命令。u 代表是给当前使用的用户，该user用户，修改，+ 就是加，给它添加一个权限。加一个x权限。x为可以执行的权限。
     chmod g+w // 用户组的可写权限打开。
     chmod o+wx // 其他用户的写、执行权限打开。
     chmod a-x // 全部的可执行权限关闭。
     chmod u=rwx // 将u（当前用户的rwx可读、可写、可执行）权限设置为打开。
     chmod u=rwx g=rw o=rwx // 可以多个修改。
     ```

   - 使用数字代表权限。`r = 4，w = 2， x = 1`。设置多权限就把对应的数组加起来。如下：
   
     ```js
     chmod 777 test // 修改test文件夹的权限为 a（所以用户）rwx。可读、可写、可执行。这里的第一个7代表的是u（user自己）、第二个7代表的是g（用户组）、第三个o（他们、其他人）
     chmod 774 test // 意思为：u（自己）和g（组）权限为可读可写，o（其他人）权限为只读。
     chmod 444 test // 包括自己在内的所有人员权限为：只读。
     chmod 764 test // u（自己）可读可写可执行，g（组）可读可写 不可执行，o（其他人）只能读。
     chmod -r 444 test // 加上一个-r是代表把文件夹下面的文件及文件夹的权限都改了。
     ```
   
     这里只有三个数字是因为一个数字代表三个`-`。具体的权限看他的数字的总和。
   
   - 修改所属人、所属组。
   
     1. **chown**：修改所属人。
   
        这里需要注意的是，修改所属人估计权限不够，所以我们在前面加一个sudo。
   
        ```js
        sudo chown user test // 修改test文件夹的所属人为user
        ```
   
     2. **chgrp**：修改所有组。
   
        也是权限不够，需要在前面加上sudo。
   
        ```js
        sudo chgrp user test // 修改test文件夹的所属组为user
        ```
   
        <img src="../../../../images/扩展知识/Linux/image-20210528112234389.png" alt="image-20210528112234389" style="zoom:;" />
   
        也都可以加上**-r**，递归。也就是所有的子文件、子文件夹都修改问这个所属用户、所属组。

# 在Linux系统中安装Tomcat

## 安装JDK

安装tomcat之前，必须要安装JDK。

### 使用yum一键安装

~~~shell
yum install -y java-1.8.0-openjdk-devel // 这里装完以后记得去配置jdk环境变量
~~~

### 查看java版本

~~~shell
java -version
~~~

## 配置环境变量

### 找到java安装的路径

~~~shell
whereis java // 查看路径
// /usr/bin/java /usr/lib/java /etc/java /usr/share/java /usr/share/man/man1/java.1.gz

 ls -lrt /usr/bin/java // 查看java的bin之下路径
// /usr/bin/java -> /etc/alternatives/java

ls -lrt /etc/alternatives/java // 查看需要配置环境的路径
 // /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.212.b04-0.el7_6.x86_64/jre/bin/java
/usr/lib/jvm/jre-1.7.0-openjdk.x86_64/bin/java
~~~

### 进入文件夹配置环境变量

~~~shell
vim /etc/profile // 进入java环境变量配置单的文件
~~~

`在文件的末尾处添加以下代码：`

~~~shell
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.302.b08-0.el8_4.x86_64
export PATH=$JAVA_HOME/jre/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
~~~

`注意：`上面代码的第一行，**export JAVA_HOME=**之后，改为你自己的路径，切注意，路径不包含版本号、系统号之后的`/jre/bin/java` 这个路径。

### 使配置生效

~~~shell
source /etc/profile
~~~

### 查看JAVA_HOME环境变量

~~~shell
echo $JAVA_HOME
// /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.212.b04-0.el7_6.x86_64
~~~

# 下载Tomcat

进入Tomcat官网下载页面，下载需要的版本的Tomcat。官网地址：[Tomcat](https://tomcat.apache.org/download-80.cgi)

# 安装Tomcat

把下载好的压缩包，上传到Linux系统中。

1. 创建目录

   ~~~shell
   mkdir /usr/local/tomcat/
   ~~~

2. 解压到需要安装的目录

   ~~~shell
   tar -zxvf apache-tomcat-8.5.49.tar.gz -C /usr/local/tomcat/
   ~~~

   解压缩以后，进入/usr/local/tomcat/目录后，你会发现多一个目录，它就是Tomcat所在目录。Tomcat版本不同，这个目录名有所不同，这里是**apache-tomcat-8.5.49**。

3. 启动

   执行Tomcat的启动脚本

   ~~~shell
   /usr/local/tomcat/apache-tomcat-8.5.49/bin/startup.sh
   ~~~

   返回的结果如下：

   ~~~shell
   Using CATALINA_BASE:   /usr/local/tomcat/apache-tomcat-8.5.49
   Using CATALINA_HOME:   /usr/local/tomcat/apache-tomcat-8.5.49
   Using CATALINA_TMPDIR: /usr/local/tomcat/apache-tomcat-8.5.49/temp
   Using JRE_HOME: /usr/local/java/jdk1.8.0_231/jre
   Using CLASSPATH: /usr/local/tomcat/apache-tomcat-8.5.49/bin/bootstrap.jar:/usr/local/tomcat/apache-tomcat-8.5.49/bin/tomcat-juli.jar
   Tomcat started.
   ~~~

   启动完成以后。

4. 验证

   Tomcat默认端口是8080，在浏览器中输入对应IP和端口，比如：http://192.168.1.111:8080，就可以访问了

# 在Tomcat上部署项目

把需要部署的项目放到webapp目录之下。这时候我们输入自己的ip:8080/项目文件名/index.html可以正常的查看到我们的项目。但这个时候，我们发现，在访问我们的项目内容时，必须加上我们的项目名字"myweb"，这样很不好。

1. 我们可以编辑conf/server.xml进行配置，打开server.xml文件，找到Host元素，默认配置如下：

   ~~~shell
    <Host name="localhost"  appBase="webapps"
            unpackWARs="true" autoDeploy="true">
       <Context docBase="myProject" path=""/>
   
       <!-- SingleSignOn valve, share authentication between web applications
            Documentation at: /docs/config/valve.html -->
       <!--
       	<Valve className="org.apache.catalina.authenticator.SingleSignOn" />
        -->
   
       <!-- Access log processes all example.
            Documentation at: /docs/config/valve.html
            Note: The pattern used is equivalent to using pattern="common" -->
       <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
              prefix="localhost_access_log" suffix=".txt"
              pattern="%h %l %u %t &quot;%r&quot; %s %b" />
    </Host>
   
   ~~~

   我们需要在Host内部增加Context的内容，增加之后如下：

   ~~~shell
    <Host name="localhost"  appBase="webapps"
            unpackWARs="true" autoDeploy="true">
       <Context docBase="myProject" path=""/>
   
       <!-- SingleSignOn valve, share authentication between web applications
            Documentation at: /docs/config/valve.html -->
       <!--
       	<Valve className="org.apache.catalina.authenticator.SingleSignOn" />
        -->
   
       <!-- Access log processes all example.
            Documentation at: /docs/config/valve.html
            Note: The pattern used is equivalent to using pattern="common" -->
       <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
              prefix="localhost_access_log" suffix=".txt"
              pattern="%h %l %u %t &quot;%r&quot; %s %b" />
    </Host>
   
   ~~~

   这个时候，就可以通过这种不用加项目名的http://localhost:8080/index.html形式访问了

   这里需要==注意：==的是

   ~~~shell
   <Context docBase="myProject" path=""/>
   ~~~

   docBase后面跟的是我们的项目名称。



# Linux下重启Tomcat

1. 进入linux系统下Tomcat的bin目录

   ~~~shell
   /usr/local/tomcat/apache-tomcat-8.5.30/bin
   ~~~

2. 关闭一下Tomcat服务，特别是已经启动的情况下，只不过有些异常

   ~~~shell
   ./shutdown.sh
   ~~~

3. 检查一下tomcat是否确实已经关闭

   ~~~shell
   ps -ef | grep java
   ~~~

   假如出现以下类似的提示，表示tomcat已经关闭

   `root       16117   16036  0 13:51 pts/0    00:00:00 grep --color=auto java`

4. 最后重新启动tomcat

   ~~~shell
   ./startup.sh
   ~~~

   

# Tomcat部署域名+证书

部署步骤：

1. 搭建Tomcat环境。
2. 申请域名证书。
3. 部署域名的http访问。
4. 部署域名的https访问。
5. 强制使http跳转至https。

我这里从第三步开始。

## 部署域名的http访问。

 部署好Tomcat后，找到对应目录下的conf文件找到server.xml文件修改对应的配置。找到Host添加域名绑定配置

~~~shell
<Host name="www.xn--xkr52xh3grqg.cn"  appBase="webapps"
              unpackWARs="true" autoDeploy="true">
        <Context docBase="myProject" path=""/>

        <!-- SingleSignOn valve, share authentication between web applications
             Documentation at: /docs/config/valve.html -->
        <!--
        <Valve className="org.apache.catalina.authenticator.SingleSignOn" />
        -->
        
        <!-- Access log processes all example.
             Documentation at: /docs/config/valve.html
             Note: The pattern used is equivalent to using pattern="common" -->
        <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
               prefix="localhost_access_log" suffix=".txt"
               pattern="%h %l %u %t &quot;%r&quot; %s %b" />

</Host>
~~~

`配置详情：`

~~~shell
 <Host name="域名"  appBase="webapps"
	 unpackWARs="true" autoDeploy="true">
 	 <Context path="" docBase="网站文件路径"/>
 </Host>
~~~

测试域名访问成功后，进行下一步测试。

## 配置域名https访问

将域名的ssl证书放到Tomcat中的conf文件中。在server.xml文件中找到ssl配置中做如下配置修改：

~~~shell
<Connector port="443" protocol="org.apache.coyote.http11.Http11NioProtocol"
               maxThreads="150" SSLEnabled="true" defaultSSLHostConfigName="www.xn--xkr52xh3grqg.cn">
        <SSLHostConfig hostName="www.xn--xkr52xh3grqg.cn">
            <Certificate certificateKeystoreFile="conf/qianmonianhua.jks" certificateKeystorePassword="123456"
                         type="RSA" />
        </SSLHostConfig>
</Connector>
~~~

这一段仔细找，默认是写好了的。但是是注释的。我们需要把注释符号去掉。

`配置详情：`

~~~shell
<Connector port="443" protocol="org.apache.coyote.http11.Http11Nio2Protocol" maxThreads="150" SSLEnabled="true" defaultSSLHostConfigName="域名">   
  <SSLHostConfig hostName="域名">   
    <Certificate certificateKeystoreFile="conf/证书路径以及名称" certificateKeystorePassword="证书密码" type="RSA"/>   
  </SSLHostConfig>      
</Connector>
~~~

这里一定不要忘了第一行上面的 `defaultSSLHostConfigName="域名"`，否则会出现404！

为了做强制https。所以我也在这时候修改了如下配置：

```shell
<Connector port="80" protocol="HTTP/1.1"
    connectionTimeout="20000"
    redirectPort="443" />
```

redirectPort改成ssl的connector的端口443，重启后便会生效

## 强制使http跳转至https

到conf目录下的web.xml。在</welcome-file-list>后面，</web-app>，也就是倒数第二段里，加上这样一段

~~~shell
<login-config>
    <!-- Authorization setting for SSL -->
    <auth-method>CLIENT-CERT</auth-method>
    <realm-name>Client Cert Users-only Area</realm-name>
    </login-config>
    <security-constraint>
    <!-- Authorization setting for SSL -->
    <web-resource-collection>
    <web-resource-name>SSL</web-resource-name>
    <url-pattern>/*</url-pattern>
    </web-resource-collection>
    <user-data-constraint>
    <transport-guarantee>CONFIDENTIAL</transport-guarantee>
    </user-data-constraint>
    </security-constraint>
~~~

这一段在`web.xml`文件的最下面。最后的位置。加上保存即可。