---
title: Bootstarp-Vue 框架
date: 2021/03/18
categories:
- [历练ing,扩展知识,Bootstarp-Vue]
tags:
- BootstarpVue

---

1. # vue中引用bootstarpVue

   > 1. 进入你的项目里
   >
   > 2. 打开命令行工具，安装BootstrapVue,
   >
   > 3. ```javascript
   >    npm i bootstrap-vue -S
   >    ```
   >
   > 4. 安装后，打开main.js主程序入口文件
   >
   > 5. ```js
   >    import BootstrapVue from 'bootstrap-vue'
   >    
   >    import 'bootstrap/dist/css/bootstrap.css'
   >    import 'bootstrap-vue/dist/bootstrap-vue.css'
   >    
   >    // 注册为全局组件
   >    Vue.use(BootstrapVue)
   >    
   >    ```
   >
   > 6. 完成，可以直接使用它的组件了