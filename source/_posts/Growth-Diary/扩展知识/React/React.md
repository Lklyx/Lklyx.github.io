---
title: React
date: 2021/04/29
categories:
- [历练ing,扩展知识,React]
tags:
- React
---

# JsonServer

在电脑中全局装jsonServe：

```js
npm install -g json-server
```

安装好了以后在创建一个普通的db.json文件

```json
{
    "posts":[
		{"id": 1，"title": "json-server", "author": "typicode"}
    ],
	"comments":[
		{ "id": 1,"body": "some comment","postId" : 1 }
    ],
	"profile":{"name": "typiode"}
}
```

最后启动刚才创建好的jsonserver，`json-serve` + `路径` + `port 端口号`，一般就是在当前的json文件下启动，所以直接`.\`json文件名字。

```js
json-server .\test.json --port 4000 // 这里需要注意一下路径问题，相对路径。
```

## JsonServer（取、增、删、改）

1. 取数据：**get**

   ```js
   axios.get("http://localhost:3001/posts").then(res=>{
        console.log(res);
   })
   ```

2. 增：**post**

   ```js
   const params = {
   	title: '3333'，
   	author: '张三'
   }
   axios.post("http://localhost:3001/posts"，params)
   ```

3. 修改： **put**（全局更新），直接将你传入的数据替换之前存在的那一条数据，没有改的直接替换掉、删掉。例如下面的一条数据，插入以后posts接口中id为1的数据。就只有title属性了。之前的author就没有了。

   ```js
   const params = {
   	title: '3333-修改',
   }
   axios.put("http://localhost:3001/posts/1",params)
   ```

   

4. 修改-更新：**patch**（局部更新）

   ```js
   const params = {
   	title: '3333-patch修改',
   }
   axios.patch("http://localhost:3001/posts/1",params)
   ```

5. 删除：**delete**

   ```js
   axios.delete("http://localhost:3001/posts/1");
   ```

6. 表关联：**_embed（向下关联）**

   ```js
   axios.get("http://localhost:3001/posts?_embed=comments").then(res=>{
        console.log(res);
   })
   ```

7. 表关联：**_expand（向上关联）**

   ```js
   axios.get("http://localhost:3001/comments?_expand=post").then(res=>{
        console.log(res);
   })
   ```

   这里有一个一一对应的关系很微妙，要搞懂这个才知道jsonserver是怎么进行表关联的。例子：向下关联可以直接写 **_embed=comments** 因为知道json中有一个数组是comments。而向上关联则是： **_expand=post** 后面的post，是因为上一级有一个posts字段。根据这个字段找到他们之前的关联关系。

# 时间格式处理

```js
const time = (time) => {
    // time：Tue Jan 10 2023 13:43:04 GMT+0800 (中国标准时间)
    // moment：转换时间插件。moment(time).format('YYYY-MM-DD HH:mm:ss')
    // getTime()：中国标准时间转为时间搓函数，react自带的，不需要封装。time.getTime()
    return time.getTime()
 }
```

# React中页面跳转、超链接

react中点击跳转新页面的方法：

1. 页面点击本地页面打开新页面，引入ant的Button组件；

2. 本地页面不变跳转到新的页面。

   

   **页面点击本地页面打开新页面**

   ```js
   <Button style={{backgroundColor:'#F0F2F5'}}
     onClick={()=>{window.location.href="https://baidu.com"}}
     className="r-button"
   >
   ```

   引入**import {Link} from 'react-router-dom'**

   ```js
   <Link to="/new/login/">
   <Button className="e-button" type="primary">Back to login page</Button>
   </Link>
   ```

   **本地页面不变跳转到新的页面**

   ```js
   <Button style={{backgroundColor:'#F0F2F5'}}
   onClick={this.handle}
   className="last-button"
   >
   handle=()=>{
     const w=window.open('about:blank');
     w.location.href="www.baidu.com"
   }
   ```

   

