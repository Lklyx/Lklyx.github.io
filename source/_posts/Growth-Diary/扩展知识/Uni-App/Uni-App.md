---
title: Uni-app
date: 2021/04/06
categories:
- [历练ing,扩展知识,Uni-app]
tags:
- Uni-app
---

`学习视屏21集开始`

[学习视屏连接](https://www.bilibili.com/video/BV1BJ411W7pX?p=21&spm_id_from=pageDriver)

# 数据缓存

本章主要讲到[uni-app官方文档](https://uniapp.dcloud.io/api/storage/storage?id=setstorage)中的APi之下的数据缓存。介绍了以下三个的用法

1. **uni-setStorage**
2. **uni-getStorage**
3. **uni-removeStorage**

uni-setStorage和uni-setStorageSync的区别在于没有带Sync的是异步的方法，带Sync的是同步的方法，常用的是同步的方法。

# 上传图片

本章主要讲到[uni-app官方文档](https://uniapp.dcloud.io/api/storage/storage?id=setstorage)中的APi之下的媒体之下的图片。主要注意看参数表格。默认最大是9张图

文档中的[uni.chooseImage](https://uniapp.dcloud.io/api/media/image?id=chooseimage)是从本地相册选择图片或者是使用相机拍照。

**OBJECT 参数说明**

| 参数名     | 类型          | 必填 | 说明                                                         | 平台差异说明                              |
| :--------- | :------------ | :--- | :----------------------------------------------------------- | :---------------------------------------- |
| count      | Number        | 否   | 最多可以选择的图片张数，默认9                                | 见下方说明                                |
| sizeType   | Array<String> | 否   | original 原图，compressed 压缩图，默认二者都有               | App、微信小程序、支付宝小程序、百度小程序 |
| extension  | Array<String> | 否   | 根据文件拓展名过滤，每一项都不能是空字符串。默认不过滤。     | H5(HBuilder X2.9.9+)                      |
| sourceType | Array<String> | 否   | album 从相册选图，camera 使用相机，默认二者都有。如需直接开相机或直接选相册，请只使用一个选项 |                                           |
| success    | Function      | 是   | 成功则返回图片的本地文件路径列表 tempFilePaths               |                                           |
| fail       | Function      | 否   | 接口调用失败的回调函数                                       | 小程序、App                               |
| complete   | Function      | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |                                           |

**success 返回参数说明**

| 参数          | 类型                       | 说明                                       |
| :------------ | :------------------------- | :----------------------------------------- |
| tempFilePaths | Array<String>              | 图片的本地文件路径列表                     |
| tempFiles     | Array<Object>、Array<File> | 图片的本地文件列表，每一项是一个 File 对象 |

**File 对象结构如下**

| 参数 | 类型   | 说明                           |
| :--- | :----- | :----------------------------- |
| path | String | 本地文件路径                   |
| size | Number | 本地文件大小，单位：B          |
| name | String | 包含扩展名的文件名称，仅H5支持 |
| type | String | 文件类型，仅H5支持             |

**示例**

```javascript
uni.chooseImage({
    count: 6, //默认9
    sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
    sourceType: ['album'], // 从相册选择
    success: function (res) {
        console.log(res.tempFilePaths); // 打印出上传图片的路径。路径为一个数组，这是我们可以在data中声明一个数组，将上传的图片路径赋值（这里使用箭头函数，要不然this指向会出错）到这个数组中，再渲染出来，就可以查看到上传的图片了。
    }
});
```

# 23.条件注释实现跨端兼容

使用注释，在==`注释中`==添加他的`平台标识`，以`#ifdef`开头，以`#endif`结尾。

# 24.导航跳转

有声明式导航和编程式导航。

声明式：直接用`navogator`标签来跳转，

编程式：给当前需要跳转的图片、文字、按钮一个方法，在方法中写

```javascript
//在起始页面跳转到test.vue页面并传递参数
uni.navigateTo({
    url: 'test?id=1&name=uniapp' // 需要跳转的地址
});
```

跳转时传参数，只需在url后面，用`问号？`+ 需要传递过去的“参数名”=“参数值”，多个参数用`&`隔开。例子如下：

```javascript
url:'/pages/detail/detail?id=80&age=20' 
// 跳转时，传递一个id等于80和age等于20的值过去
```

在传过去以后，接受页面跳转传过来的参数保存在`onLoad`生命周期函数参数中的`options`中，例子如下：

```javascript
expord defaule {
	onLoad(options){
		console.log(options)
	}
}
```

# 25.组件中的生命周期函数

和vue中的一样。但是，其中页面数据发生改变之前，和页面数据发生改变之后两个生命周期函数只在安卓程序中能使用。