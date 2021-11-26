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

## 利用css画三角形



> 1. html
>
>    ```html
>      <view class="xiansh">
>        <view class="up sanjiao"></view>
>        <view class="down sanjiao"></view>
>        <view class="left sanjiao"></view>
>        <view class="right sanjiao"></view>
>      </view>
>    ```
>
> 2. css
>
>    ```css
>    .xiansh{
>      margin: 0 auto;
>      width: 400rpx;
>      overflow: hidden;
>      position: relative;
>    }
>    .sanjiao{
>      border-style: solid;
>      border-color: transparent transparent #cccccc;
>    }
>    .up{
>      position:absolute;
>      top: 82rpx;
>      left: 179rpx;
>      width: 0rpx;
>      height: 0rpx;
>      border-width: 0rpx 25rpx 25rpx;
>              
>    }
>    .down{
>      position:absolute;
>      bottom: 85rpx;
>      left: 179rpx;
>      width: 0rpx;
>      height: 0rpx;
>      transform: rotate(180deg);
>      border-width: 0rpx 25rpx 25rpx;
>    }
>    .left{
>      position:absolute;
>      top: 179rpx;
>      left: 70rpx;
>      width: 0rpx;
>      height: 0rpx;
>      transform: rotate(-90deg);
>      border-width: 0rpx 25rpx 25rpx;
>    }
>    .right{
>      position:absolute;
>      top: 179rpx;
>      right: 70rpx;
>      width: 0rpx;
>      height: 0rpx;
>      transform: rotate(90deg);
>      border-width: 0rpx 25rpx 25rpx;
>    }
>    ```

## 给div加阴影

> box-shadow:2px 2px 10px #909090;
>
> 第一个参数是x轴阴影段长度
>
> 第二个参数是y轴阴影段长度
>
> 第三个参数是往四周阴影段长度
>
> 第四个参数是阴影段颜色

## 标题超出多少行用…显示

> ```css
> display: -webkit-box;
>    overflow: hidden;
>    -webkit-box-orient: vertical;
>    -webkit-line-clamp: 2; // 后面的数字代表第几行后面为...
> ```
>
> 标题和表格中，文字超出一定长度后省略，使用`…`代替。

## 首行缩进2字符，或者第二行缩进2字符

> 我们知道**css**中**text-indent**属性可以使每个段落首行开头文字缩进，如缩进2个文字距离样式。
>
> ```css
> p{
> 	text-indent: 2em; /*em是相对单位*/
> }
> ```
>
> 注：em是相对长度单位。相对于当前对象内文本的字体尺寸。我们中文段落一般每段前空两个汉字。实际上，就是首行缩进了**2em**。
>
> 那如果我们想让第二行缩进一格呢?
>
> ```css
> p {
> 　　text-indent: -2em;
> 　　margin-left: 2em; /*padding-left:2em*/
> }
> ```
>
> 设置text-indent: -2em;以后p标签中第一行文字向左偏移，这样第二行开始的文字就等于缩进了，
> 但是这样设置会导致第一行向左超出div，所以再用margin-left使p标签整体右移即可，不过也可以用 padding-left:2em ，这样IE8里也能显示。

