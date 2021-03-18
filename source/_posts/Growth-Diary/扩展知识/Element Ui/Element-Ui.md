---
title: Element-Ui 框架
date: 2021/03/18
categories:
- [历练ing,扩展知识,Element-Ui]
tags:
- ElementUi

---

# 自定义表格内外边框颜色

## 问题描述

在我们使用饿了么UI框架做项目的时候，el-table的自带的表格边框颜色有时候需要修改一下。本文简述一下修改el-table边框样式的注意事项。

### 初始代码

```vue
<template>
  <div id="app">
    <el-table 
      :data="tableData" 
      style="width: 40%" 
      border
    >
      <el-table-column prop="name" label="姓名" width="180"></el-table-column>
      <el-table-column prop="nation" label="国别" width="180"></el-table-column>
      <el-table-column prop="bornPlace" label="出生地方"> </el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      tableData: [
        {
          name: "刘备",
          nation: "蜀国",
          bornPlace: "涿郡涿县（河北省涿州市）",
        },
        {
          name: "曹操",
          nation: "魏国",
          bornPlace: "沛国谯县（安徽省亳州市）",
        },
        {
          name: "孙权",
          nation: "吴国",
          bornPlace: "吴郡富春县（浙江省杭州市富阳区）",
        },
        {
          name: "关羽",
          nation: "蜀国",
          bornPlace: "河东郡解县（山西省运城市盐湖区解州镇）",
        },
      ],
    };
  },
};
</script>
```

### 初始效果

![image](https://image-static.segmentfault.com/116/486/1164868583-600e6388628a4)

### 第一步，加入单元格的回调

#### 代码如下

![image](https://image-static.segmentfault.com/393/733/3937331683-600e642992093)

#### 效果如下

![image](https://image-static.segmentfault.com/384/833/3848336474-600e64951e0a1)

### 第二步，加入表头的回调

#### 代码如下

![image](https://image-static.segmentfault.com/364/434/364434355-600e654c78c83)

#### 效果如下

![image](https://image-static.segmentfault.com/248/389/2483891796-600e65a2a71b7)

### 第三步，单独给表格加样式

#### 代码如下

![image](https://image-static.segmentfault.com/200/720/200720399-600e67f13b8ef)
![image](https://image-static.segmentfault.com/405/061/4050614932-600e67c3c88e5)

#### 效果如下

![image](https://image-static.segmentfault.com/179/167/1791671657-600e681be28ab)