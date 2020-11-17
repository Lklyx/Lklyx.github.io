---
title: css知识点
date: 2020/11/17
categories:
- [历练ing,CSS]
tags:
- css
---

# 在vue中如何让背景图片填满整个屏幕

> `代码如下`
>
> ```css
> .backimg {
>   background-image: url('../../assets/smarthome/隔离透明背景.png');
>   height: 100%;
>   width: 100%;
>   background-size: 100% 100%;
>   position: fixed;
>   width: 100%;
> }
> ```
>
> 新建一个div，使这个div的宽高都为100%，设置背景图片，背景图片的大小设置为宽高100%，最后使用`position: fixed;`属性，让这个新建的div脱离文档流，如果有其他的定位属性，可以给当前的div添加z-`index: -1`;