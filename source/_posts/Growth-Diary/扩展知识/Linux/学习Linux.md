---
title: 学习Linux
date: 2021/05/19
categories:
- [历练ing,扩展知识,Linux]
tags:
- Linux
---

# linux文件系统

linux中没有盘符的概念，只有一个根目录。根目录用`/`表示。

1. `/`根目录下有以下几个文件。

   - `/bin`
   - `/etc`
   - `/home`
   - `/lib`
   - `/usr`

   这些不同的目录都有不同的作用。每个目录的作用介绍可查看[Linux目录介绍](http://www.cnblogs.com/duanji/p/yueding2.html)

2. Linux常用目录

   - **pwd**查看当前在那个目录以及是那个用户。
   - **ls**查看当前目录下有那些文件夹，有颜色的或者有后缀名的是文件夹，可以打开，没有的是文件。
   - **cd**进入到文件夹。进去了之后可以用`pwd`查看，==注意：==区分大小写

