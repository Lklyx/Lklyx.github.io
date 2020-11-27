---
title: css知识点
date: 2020/11/17
categories:
- [历练ing,CSS]
tags:
- css
---

## 在vue中如何让背景图片填满整个屏幕

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

## 设置字体颜色为渐变色

> ```css
> .title{
>     background-image: linear-gradient(180deg,red,blue);
>     -webkit-background-clip:text;
>     color: transparent;
>  }
> ```
>
> **background-image属性：设置背景图片为线性渐变色**
>
> **background-clip 属性：规定背景的绘制区域****(我们注意到该属性上的-webkit-，说明该属性还存在兼容问题，并不是所有浏览器都支持，在W3C是没有text这个值的，这里的text是背景被裁剪到文字)
>
> **color属性: 设置文字颜色为透明，然后面的背景色显示出来。**
>
> **180deg**：设置渐变开始的角度

