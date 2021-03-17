---
title: GitHub中遇到的问题
date: 2021/03/17
categories:
- [历练ing,Blog]
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

