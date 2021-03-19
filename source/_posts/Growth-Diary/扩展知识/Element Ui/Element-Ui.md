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

# 表格自适应宽

```html

<template>
<!-- 表格的自适应宽 -->
<div class="container">

   <h2>All Columns auto-fit</h2>
   <el-button @click="handleAddColumn" type="primary">Add Column</el-button>
  <el-button @click="handleAddRows" type="success">Add Row</el-button>
  <el-table
    :data="data"
    border
    auto-fit-column
  >
    <el-table-column
      label="姓名2222"
      prop="name"
      fixed
    ></el-table-column>
    <el-table-column
      label="年龄3333"
      prop="age"
    ></el-table-column>
    <el-table-column
      v-for="(option, index) in options"
      :label="option.label"
      :prop="option.prop"
      :key="index"
      sortable
      auto-fit
    ></el-table-column>
    <el-table-column
      label="年龄"
      width="100"
    >
      <template slot="header">
        <el-input
          v-model="search"
          size="mini"
          placeholder="Type to search"/>
      </template>
    </el-table-column>
  </el-table>

  <h2>Max-width</h2>
  <el-table
    :data="data"
    border
    auto-fit-column
  >
    <el-table-column
      label="姓名2222"
      prop="name"
      fixed
    ></el-table-column>
    <el-table-column
      label="年龄3333"
      prop="age"
      :max-width="130"
    ></el-table-column>
    <el-table-column
      v-for="(option, index) in options"
      :label="option.label"
      :prop="option.prop"
      :key="index"
      :max-width="100"
      sortable
      auto-fit
    ></el-table-column>
    <el-table-column
      label="年龄"
      width="100"
    >
      <template slot="header">
        <el-input
          v-model="search"
          size="mini"
          placeholder="Type to search"/>
      </template>
    </el-table-column>
  </el-table>

  <h2>Some Columns auto-fit (name & age)</h2>

  <el-button @click="handleAddColumn" type="primary">Add Column</el-button>
  <el-button @click="handleAddRows" type="success">Add Row</el-button>
  <el-table
    :data="data"
    border
    auto-fit-column
    :fit-styles="styles"
    :fit-columns="['name', 'age', 'salary']"
  >
    <el-table-column
      label="Name"
      prop="name"
      fixed
    ></el-table-column>
    <el-table-column
      label="Age"
      prop="age"
    ></el-table-column>
    <el-table-column
      label="Salary"
      prop="salary"
      :formatter="formatter"
    ></el-table-column>
    <el-table-column
      v-for="(option, index) in options"
      :label="option.label"
      :prop="option.prop"
      :key="index"
      sortable
      auto-fit
    ></el-table-column>
    <el-table-column
      label="年龄"
      width="100"
    >
      <template slot="header">
        <el-input
          v-model="search"
          size="mini"
          placeholder="Type to search"/>
      </template>
    </el-table-column>
  </el-table>

   <h2>Show Summary</h2>

  <el-button @click="handleAddColumn" type="primary">Add Column</el-button>
  <el-button @click="handleAddRows" type="success">Add Row</el-button>
  <el-button @click="handleReverseColumn" type="success">Reverse Column</el-button>
  <el-button @click="handleDynamicAutoColumn" type="success">Dynamic auth-width Column</el-button>
  <el-table
    :data="data"
    border
    auto-fit-column
    show-summary
    :summary-method="summaryMethod"
    :fit-styles="styles"
    :fit-columns="fitColumns"
  >
    <el-table-column
      v-for="(column, cIndex) in autoWidthColumns"
      :label="column.label"
      :prop="column.name"
      :key="cIndex"
      :formatter="formatter"
      fixed
    ></el-table-column>
    <el-table-column
      v-for="(option, index) in options"
      :label="option.label"
      :prop="option.prop"
      :key="10 + index"
      sortable
      auto-fit
    ></el-table-column>
    <el-table-column
      label="年龄"
      width="100"
    >
      <template slot="header">
        <el-input
          v-model="search"
          size="mini"
          placeholder="Type to search"/>
      </template>
    </el-table-column>
  </el-table>

  <div class="copyright">&copy; www.kuaizi.ai</div>
</div>
</template>

<script>
const currency = (num, decimal = 2) => {
  let n = Number(num)
  let parts
  let hasDecimal = false
  if (num !== null && !isNaN(n)) {
    // 检测是否有小数点
    hasDecimal = /\.\d{1,}/g.test(num)
    // 精度
    n = hasDecimal ? n.toFixed(decimal) : String(n)
    parts = n.split('.')
    return `${parts[0].replace(/\B(?=(\d{3})+(?!\d))/g, ',') + (hasDecimal ? '.' : '') + (parts[1] || '')}`.replace(/\.$/, '')
  }
  return '-'
}
export default {
  data () {
    return {
      search: '',
      data: [
        {
          name: '张三',
          age: 30,
          salary: 320000,
          remark: 'sdfsdfsdfsdfsdfsdff'
        },
        {
          name: '李四',
          age: 24,
          salary: 525000,
          remark: 'sdfsdfsdfsdfsdfsdff'
        }
      ],
      options: [],
      autoWidthColumns: [
        {
          name: 'name',
          label: 'Name'
        },
        {
          name: 'age',
          label: 'Age'
        },
        {
          name: 'salary',
          label: 'Salary'
        },
        {
          name: 'remark',
          label: 'Remark'
        }
      ],
      styles: {
        header: 'font-size: 14px; font-weight: bold; padding: 0 10px;',
        body: 'font-size: 14px; padding: 0 10px;'
      }
    }
  },
  computed: {
    fitColumns () {
      return this.autoWidthColumns.map(a => a.name)
    }
  },
  methods: {
    // formatter (row, column, cellValue, index) {
    formatter (row, column, cellValue) {
      if (column.property !== 'salary') return cellValue
      // 获取字段名
      // console.log(column.property)
      return currency(cellValue)
    },
    handleAddColumn () {
      this.options.push({ prop: 'remark', label: '备注', maxWidth: 130 })
    },
    handleAddRows () {
      this.data.push({
        name: 'tommyshao',
        age: 30,
        salary: 15000,
        remark: 'sdfsdfsdf什么备注，不准换行啊啊啊啊啊啊啊啊啊啊啊'
      })
    },
    summaryMethod ({ columns, data }) {
      const showSummaryCol = ['salary']
      const sums = []
      columns.forEach((column, index) => {
        if (index === 0) {
          sums[index] = '合计'
          return
        }
        const values = data.map(item => Number(item[column.property]))
        if (!values.every(value => isNaN(value)) && showSummaryCol.includes(column.property)) {
          sums[index] = values.reduce((prev, curr) => {
            const value = Number(curr)
            if (!isNaN(value)) {
              return prev + curr
            } else {
              return prev
            }
          }, 0)
          sums[index] = currency(sums[index])
        } else {
          sums[index] = ''
        }
      })
      return sums
    },
    handleReverseColumn () {
      // this.autoWidthColumns =
      this.autoWidthColumns.reverse()
    },
    handleDynamicAutoColumn () {
      this.autoWidthColumns = [
        {
          name: 'remark',
          label: 'Remark'
        },
        ...this.autoWidthColumns.slice(0, 2)
      ]
    }
  }
}
</script>

<style>
.container {
  overflow-x: auto;
}
.el-table .cell {
  white-space: nowrap;
}
.copyright {
  text-align: center;
  margin: 100px 20px 20px;
  padding: 20px 0 0;
  border-top: 1px solid #e7e7e7;
}
</style>

```

