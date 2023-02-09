---
title: JS-封装的方法
date: 2023/02/09
categories:
- [历练ing,扩展知识,JavaScript]
tags:
- JavaScript
---

# 计算当前时间是今天的第几秒？

```js
// 计算当前时间的秒数 （16:25:32）
  const formatHMStoS = (value) => {
    var h, m, s = 0
    if (value.indexOf(":") != -1) {
      h = value.split(":")[0];
      m = value.split(":")[1]
      s = value.split(":")[2]
    } else if (value.indexOf(":") == -1) {
      if (value.indexOf(":") == -1) {
        h = 0
        m = 0
        s = value.split(':')[0];
      } else {
        h = 0
        m = value.split(':')[0];
        s = value.split(':')[1];
      }
    }
    var ss = h * 60 * 60 + m * 60 + s * 1;
    return ss;
  }
```