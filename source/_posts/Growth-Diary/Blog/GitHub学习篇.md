---
title: GitHub中遇到的问题
date: 2021/03/17
categories:
- [历练ing,Blog,工具]
tags:
- GitHub

---

# 打不开GitHub官网

1. 百度搜*索查询网址dns*，或者直接打开[网址查询](https://tool.chinaz.com/dns/)

2. 检测到[https://github.com](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com)网址响应的IP，将得到的IP添加到hosts文件中去。

3. hosts文件路径为：电脑磁盘中`windows C:\Windows\System32\drivers\etc\hosts`右击，以管理员身份打开，打开方式为记事本。将上面查询到的IP地址输入到文件中保存即可。

4. 现在我加入的是：

   > 13.229.188.59 github.com
   > 140.82.112.4 github.com
   
5. 如果还是不行，那就借阅这位博主的地址：https://zhuanlan.zhihu.com/p/107334179?ivk_sa=1024320u。

6. `工具`：

   这里我们可以借助一个工具来更新自己电脑里面的host文件。不用每次去找路径在以管理员身份打开，简化了很多繁琐的步骤**:SwitchHosts**，直接去官网下载就可以了。也可以到我的百度网盘自己提取，下面附上我的百度网盘地址。

   > 链接：https://pan.baidu.com/s/1J-UspFd82wENMxjGE4RP4g 
   > 提取码：arp0 

