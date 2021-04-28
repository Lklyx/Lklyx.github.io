---
title: webpack打包工具
date: 2021/03/26
categories:
- [历练ing,扩展知识,Webpack]
tags:
- Webpack

---

#  webpack五个核心概念

1. Entry

   入口（Entry）指示Webpack以那个文件为入口起点开始打包，分析构建内部依赖图。从哪儿打包。

2. Output

   输出（Output）指示webpack打包后的资源bundles输出到哪里去，以及如何命名。

3. Loader

   Loader让Webpack能够去处理那些非JavaScript文件（Webpack）自身只理解JavaScript文件。就是翻译css。以及茹铺，让他成为Webpack可以认识的东西。

4. Plugins

   插件（Plugins）可以用于执行范围更广的任务。插件的范围包括，从打包优化和压缩，一直到重新定义环境中的变量等。做些功能更加强大的事。

5. Mode

   模式（Mode）指示Webpack使用相应的模式配置。

   - development

     测试环境，能让代码本地调试、运行的环境，配置相对来说，简单一点。

   - production

     生产环境，能让代码优化上线，运行的环境。优化更好。配置也比较全面。