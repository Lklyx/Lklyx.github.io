---
title: 绑定事件，根据下标判断当前的元素。
date: 2020/11/23
categories:
- [历练ing,VUE]
tags:
- VUE
- 成长
---
## vue渲染页面

用一个`li`渲染八个list小div，当鼠标放上去的时候，给他们绑定两个事件，一个移入事件，一个移除事件。首先，用css的`hover`属性给每一个div添加一个背景图片，鼠标放上去的时候背景为灰色。移开就恢复黑色。

1. 效果图如下：

   ![image-20201123143929661](../../../../images/vue/image-20201123143929661.png)

2. 代码如下：

   ```html
   <template>
     <section>
       <div class="card">
         <ul>
           <li v-for="(item,index) of list" @mouseover="yiru(index)" @mouseleave="yichu(index)" :key="item.id" class="list">
             <img :src="item.imgsrc" alt="">
             <span>{{ item.text }}</span>
             <div v-if="item.isactive" class="setup"><img src="../../assets/smarthome_index/控制面板图标.png" alt=""></div>
           </li>
         </ul>
       </div>
     </section>
   </template>
   ```

   ```javascript
   <script>
     export default{
       data() {
         return{
           list:[
             {id:'1', imgsrc: require('../../assets/smarthome_index/线性吊灯图标.png'), text: '灯光', isactive: false },
             {id:'2', imgsrc: require('../../assets/smarthome_index/窗帘图标.png'), text: '窗帘', isactive: false },
             {id:'3', imgsrc: require('../../assets/smarthome_index/空调图标.png'), text: '空调', isactive: false },
             {id:'4', imgsrc: require('../../assets/smarthome_index/电视机图标.png'), text: '电视', isactive: false },
             {id:'5', imgsrc: require('../../assets/smarthome_index/音响图标.png'), text: '音响', isactive: false },
             {id:'6', imgsrc: require('../../assets/smarthome_index/门锁图标.png'), text: '门锁', isactive: false },
             {id:'7', imgsrc: require('../../assets/smarthome_index/添加设备图标.png'), text: '添加设备', isactive: false },
             {id:'8', imgsrc: require('../../assets/smarthome_index/其它图标.png'), text: '其它', isactive: false }
           ]
         }
       },
       methods:{
         yichu(index){
           this.list[index].isactive = false
         },
         yiru(index){
           this.list[index].isactive = true
           console.log(index);
         }
       }
     }
   </script>
   ```

   ```css
   <style scoped>
     .card{
       width: 1200px;
       /* border: 1px solid red; */
       margin: auto;
       overflow: hidden;
       display: flex;
       align-items: center;
       position: relative;
       margin-bottom: 200px;
     }
     .list{
       box-sizing: border-box;
       color: #FFFFFF;
       list-style: none;
       width: 290px;
       height: 224px;
       float: left;
       margin-right: 13.33333px;
       background-image: url(../../assets/smarthome_index/没选中背景块.png);
       padding-top: 20px;
       padding-left: 40px;
       font-size: 42px;
       position: relative;
     }
     .list img{
       display: block;
       margin-bottom: 49px;
     }
     .setup{
       position: absolute;
       top: 20px;
       right: 40px;
     }
     .list:hover{
       background-image: url(../../assets/smarthome_index/选中背景块.png);
     }
     .list:nth-child(4){
       margin-right: 0px;
       margin-bottom: 27px;
     }
     .list:nth-child(8){
       margin-right: 0px;
     }
   </style>
   ```

   鼠标放上去的时候，显示当前div右上角的设置标志。移开则恢复没有选中状态。

