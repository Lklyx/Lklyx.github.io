---
title: JavaScript
date: 2021/03/29
categories:
- [历练ing,扩展知识,JavaScript]
tags:
- JavaScript
---

# 基本语法

看阮一峰老师的笔记。[基本语法](https://javascript.ruanyifeng.com/grammar/basic.html)

# DOM概述

（DOM是操作网页的，而BOM是操作浏览器的）

1. DOM是JavaScript操作网页的接口，全称为“文档对象模型”，他的作用是将一个网页转为一个JavaScript对象，从而可以用脚本语言进行各种操作。（增删内容）。

2. DOM 的最小组成单位叫做节点（node）。文档的树形结构（DOM 树），就是由各种不同类型的节点组成。每个节点可以看作是文档树的一片叶子。

   - **Document**：整个文档树的顶层节点
   - **DocumentType：doctype**标签（比如`<!DOCTYPE html>`）
   - Element：网页的各种HTML标签（比如`<body>`、`<a>`等`）
   - **Attr**：网页元素的属性（比如class="right"）
   - **Text**：标签之间或标签包含的文本
   - **Comment**：注释
   - **DocumentFragment**：文档的片段

3. **节点树**

   一个文档的所有节点，按照所在的层级，可以抽象成一种树状结构。这种树状结构就是 DOM 树。它有一个顶层节点，下一层都是顶层节点的子节点，然后子节点又有自己的子节点，就这样层层衍生出一个金字塔结构，又像一棵树。浏览器原生提供document节点，代表整个文档。

4. **document**---整个文档树

   文档的第一层有两个节点，第一个是文档类型节点（<!doctype html>），第二个是 HTML 网页的顶层容器标签`<html>`。后者构成了树结构的根节点（root node），其他 HTML 标签节点都是它的下级节点。

   除了根节点，其他节点都有三种层级关系。

   - 父节点关系（**parentNode**）：直接的上级节点

   - 子节点关系（**childNodes**）：直接的下级节点

   - 同级节点关系（**sibling**）：拥有同一个父节点的节点

     DOM 提供操作接口，用来获取这三种关系的节点。比如，子节点接口包括firstChild（第一个子节点）和lastChild（最后一个子节点）等属性，同级节点接口包括nextSibling（紧邻在后的那个同级节点）和previousSibling（紧邻在前的那个同级节点）属性。

# DOM查询

1. **childNodes**;
   表示当前节点的所有子节点。（节点，包含空格、换行）
2. **children**;
   表示可以获取当前元素的所有子元素。（元素，标签，经常用）
3. **firstChild**;
   表示当前节点的第一个子节点。
4. **lastChild**；
   表示当前节点的最后一个子节点。
5. **parentNode**；
   表示当前节点的父节点。
6. **previousSibling**；
   表示当前节点的前一个兄弟节点。
7. **nextSibling**；
   表示当前节点的后一个兄弟节点。

# 数据类型

JavaScript 语言的每一个值，都属于某一种数据类型。JavaScript 的数据类型，共有六种。

1. 数值（number）：整数和小数

2. 字符串（string）：文本

3. 布尔值（boolean）：true和false

4. undefined：表示未定义或不存在。

5. null：表示空值。

6. 对象：（objeck）各种值组成的集合。

   其中：在对象中又分为
   （1）狭义的对象（object）
   （2）数组（array）
   （3）函数（function）

逻辑运算符
与 &&
或 ||
非 ！

相等运算符
=== 绝对相等
== 等于
！=  不等于

# 对象

1. 对象
   简单来说，对象就是一组键值对。

   键名：属性名
   键值：属性值
   对象可以是一个方法

   例：

   ```js
   var obj = {
     p:function (x) {
       return 2 * x;
     }
   };
   obj.p(1) //2
   
   ```

2. 属性的操作
   读取属性：
   采用点运算符和方括号运算符来读取属性 中的值。点运算符和方括号运算符也可以用来赋值。

   查看一个对象本身的所有属性可以用
   object.keys(对象名)

   delete命令用于删除对象的属性。删除成功后会返回true。
   例：

   ```js
   var obj = { p：1}
   delete obj.p。
   ```

   注：删除一个不存在的属性时，delete不会报错。而且也是返回一个true。

3. in 运算符
   in运算符是检查对象是否包含某个属性，注意（检查的是属性，不是属性值）如果包含就返回ture。
   例：

   ```js
   var obj = { p：1 }
   ‘p’in obj
   ```

   此时，控制台返回一个true

   for ...in 循环。
   for ...in 循环用来遍历一个对象的全部属性值。
   例：

   ```js
   var obj = {a：1，b：2，c：3}；
   for （var i in obj）{
       console.log( obj[ i ] );
   }
   ```

   此时控制台输出1,2,3

# 对象的继承

面向对象编程很重要的一个方面，就是对象的继承。A 对象通过继承 B 对象，就能直接拥有 B 对象的所有属性和方法。这对于代码的复用是非常有用的。大部分编程语言都是通过类（class）实现对象的继承。
js继承不是通过（class）而是通过原型对象（prototype）实现继承的。

1. constructor属性
   prototype对象有一个constructor属性，默认指向prototype对象所在的构造函数。

   ```js
   function P() {}
   P.prototype.constructor === P // true
   ```

   由于constructor属性定义在prototype对象上面，意味着可以被所有实例对象继承。

# 面向对象编程

1. 对象是什么？

   1. 面向对象编程。缩写为OOP，是目前主流的编程范式。它将真实世界各种复杂的关系，抽象为一个个对象，然后由对象之间的分工与合作，完成对真实世界的模拟。
   2. 每一个对象都是功能中心，具有明确分工，可以完成接受信息、处理数据、发出信息等任务。对象可以复用，通过继承机制还可以定制。因此，面向对象编程具有灵活、代码可复用、高度模块化等特点，容易维护和开发，比起由一系列函数或指令组成的传统的过程式编程（procedural programming），更适合多人合作的大型软件项目。
   3. 对象是单个实物的抽象。一本书、一辆汽车、一个人都可以是对象，一个数据库、一张网页、一个与远程服务器的连接也可以是对象。当实物被抽象成对象，实物之间的关系就变成了对象之间的关系，从而就可以模拟现实情况，针对对象进行编程。
   4. 对象是一个容器，封装了属性（property）和方法（method）。属性是对象的状态，方法是对象的行为（完成某种任务）。比如，我们可以把动物抽象为animal对象，使用“属性”记录具体是那一种动物，使用“方法”表示动物的某种行为（奔跑、捕猎、休息等等）。

2. 构造函数。

   ​		面向对象编程的第一步，就是要生成对象。前面说过，对象是单个实物的抽象。通常需要一个模板，表示某一类实物的共同特征，然后对象根据这个模板生成。
   ​		典型的面向对象编程语言（比如 C++ 和 Java），都有“类”（class）这个概念。所谓“类”就是对象的模板，对象就是“类”的实例。但是，JavaScript 语言的对象体系，不是基于“类”的，而是基于构造函数（constructor）和原型链（prototype）。
   ​		JavaScript 语言使用构造函数（constructor）作为对象的模板。所谓”构造函数”，就是专门用来生成实例对象的函数。它就是对象的模板，描述实例对象的基本结构。一个构造函数，可以生成多个实例对象，这些实例对象都有相同的结构造函数就是一个普通的函数，但是有自己的特征和用法。

   ```js
   var Vehicle = function（）{
   	this.price = 1000；
   }
   ```

   上面代码中，Vehicle就是构造函数。为了与普通函数区别，构造函数名字的第一个字母通常大写。

   构造函数的两个特点：

   - 函数体内部使用了this关键字，代表了所要生成的对象的实例。
   - 生成对象的时候，必须使用new命令。

3. new命令的原理

   使用new命令时，他后面的函数依次执行下面的步骤。

   - （1）创建一个空对象，作为将要返回的对象实例。
   - （2）将这个空对象的原型，指向构造函数的prtotype属性。
   - （3）将这个空对象赋值给函数内部的this关键字。
   - （4）开始执行构造函数内部的代码。

   也就是说，构造函数内部，this指的是一个新生成的空对象，所有针对this的操作，都会发生在这个空对象上。构造函数之所以叫“构造函数”，就是说这个函数的目的，就是操作一个空对象（即this对象），将其“构造”为需要的样子。

# BOM对象

浏览器对象模型，BOM可以使我们通过js来操作浏览器，在BOM中提供一组对象，用来完成对浏览器的操作

1. **window**

   代表的是整个浏览器的窗口，同时window也是网页中的全局对象。

2. **Navigator**

   代表的是当前浏览器的信息，通过该对象可以来识别不同的浏览器。

3. **Location**

   代表当前浏览器的地址信息，通过Location可以获取地址栏信息，或者操作浏览器跳转页面

4. **History**

   代表浏览器的历史记录，可以通过该对象来操作浏览器的历史记录，由于隐私原因，该对象不能获取到具体的历史记录，只能操作浏览器想前或者像后。而且该操作只在档次访问时有效。（关闭在打开就没有效果了）

# Date对象

Date对象是 JavaScript 原生的时间库。它以国际标准时间（UTC）1970年1月1日00:00:00作为时间的零点，可以表示的时间范围是前后各1亿天（单位为毫秒）。

1. 用法

   Date对象可以作为普通函数直接调用，返回一个代表当前时间的字符串。Date（）

   ```html
   // "Tue Dec 01 2015 09:34:43 GMT+0800 (CST)"
   ```

   无论有没有参数，返回的总是当前时间。

2. 实例方法

   Date的实例对象，有几十个自己的方法，除了**valueOf**和**toString**，可以分为以下三类。

   1. to类：从Date对象返回一个字符串，表示指定时间。
   2. get类：获取Date对象的日期和时间。
   3. set类：设置Date对象的日期和时间。

3. 拿到当前时间打印出来，输出在页面显示。

   ```javascript
   <div id="time">
   	现在还不是时间
   </div>
   	<script type="text/javascript">
   		window.onload=function(){
   			setInterval(function(){
   				times();
   			},1000);
   		}
   		function times () {
   			var uu = document.getElementById("time");
   			var today = new Date();
   			var year = today.getFullYear();
   			var yue = today.getMonth()+1;
   			var day = today.getDate();
   			var shi = today.getHours();				
   			var fen = today.getMinutes();
   			var miao = today.getSeconds();
   			var zhou = today.getDay();
   //			console.log(zhou)
   			var arr_week = new Array("星期日","星期一","星期二","星期三","星期四","星期五","星期六")
   			week = arr_week[zhou];
   			if(yue<10){
   				yue="0"+yue
   			}
   			if(miao<10){
   				miao = "0"+miao
   			}
   			if(fen<10){
   				fen = "0"+fen
   			}
   			var time = "现在是"+year+"年"+yue+"月"+day+"日"+shi+"点-"+fen+"分-"+miao+"秒-"+week
   			uu.innerHTML=time;
   		}
   	</script>
   ```

   # Math对象

   1. `Math静态方法：`
      Math对象提供以下一些静态方法。
      **Math.abs()**：绝对值
      **Math.ceil()**：向上取整
      **Math.floor()**：向下取整
      **Math.max()**：最大值
      **Math.min()**：最小值
      **Math.pow()**：幂运算
      **Math.sqrt()**：平方根
      **Math.log()**：自然对数
      **Math.exp()**：e的指数
      **Math.round()**：四舍五入
      **Math.random()**：随机数

   2. **Math.abs**
      Math.abs方法返回参数值的绝对值。

      例子：

      Math.abs(1) 	返回： 1
      Math.abs(-1)	返回： 1

   3. **Math.max( )**，**Math.min( )**:
      Math.max方法返回参数之中最大的那个值，Math.min返回最小的那个值。如果参数为空, Math.min返回Infinity, Math.max返回-Infinity。

      例子：

      > Math.max(2, -1, 5) 
      >
      > 返回： 5
      > Math.min(2, -1, 5)
      >
      >  返回： -1
      > Math.min() 
      >
      > 返回：Infinity
      > Math.max()
      >
      > 返回： -Infinity

   4. **Math.floor（）**，**Math.ceil（）**

      > 1. Math.floor方法返回小于参数值的最大整数（地板值）。
      >
      >    Math.floor(3.2) 
      >
      >    返回： 3
      >    Math.floor(-3.2) 
      >
      >    返回： -4
      >
      > 2. Math.ceil方法返回大于参数值的最小整数（天花板值）。
      >
      >    Math.ceil(3.2)
      >
      >    返回： 4
      >    Math.ceil(-3.2) 
      >
      >    返回： -3
      >    这两个方法可以结合起来，实现一个总是返回数值的整数部分的函数。
      >
      >    ```js
      >    function ToInteger(x) {
      >      x = Number(x);
      >      return x < 0 ? Math.ceil(x) : Math.floor(x);
      >    }
      >    ```
      >
      >    上面的方法传入以下参数得到的返回值如下：
      >
      >    ToInteger(3.2)	返回： 3
      >    ToInteger(3.5)	返回： 3
      >    ToInteger(3.8)	返回： 3
      >    ToInteger(-3.2)	返回：-3
      >    ToInteger(-3.5)	返回： -3
      >    ToInteger(-3.8)	返回： -3
      >
      >    上面代码中，不管正数或负数，ToInteger函数总是返回一个数值的整数部分。

   5. **Math.round（）**
      Math.round（）方法用于四舍五入。

      例子：

      Math.round(0.1)	返回：0
      Math.round(0.5) 	返回： 1
      Math.round(0.6) 	返回： 1

       等同于
      Math.floor(x + 0.5)
      注意，它对负数的处理（主要是对0.5的处理）。

      Math.round(-1.1)	返回： -1
      Math.round(-1.5)	返回： -1
      Math.round(-1.6)	返回： -2

   6. **Math.sqrt（）**
      Math.sqrt方法返回参数值的平方根。如果参数是一个负值，则返回NaN。

      Math.sqrt(4) 	返回： 2
      Math.sqrt(-4) 	返回：NaN

   7. **Math.random（）**

      Math.random（）返回0到1之间的一个伪随机数，可能等于0，但是一定小于1。

      Math.random（）返回： 0.7151307314634323

      - 任意范围内的随机数生成函数如下。

      ```js
      function getRandomArbitrary(min, max) {
      	return Math.random() * (max - min) + min;
      }
      ```

      getRandomArbitrary(1.5, 6.5)	返回：2.4942810038223864

      ------

      - 任意范围的随机整数生成函数如下。

      ```js
      function getRandomInt(min, max) {
      	return Math.floor(Math.random() * (max - min + 1)) + min;
      }
      ```

      getRandomInt(1, 6) 	返回： 5

      - 返回随机字符的例子如下：

      ```js
      function random_str(length) {
        var ALPHABET = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
        ALPHABET += 'abcdefghijklmnopqrstuvwxyz';
        ALPHABET += '0123456789-_';
        var str = '';
        for (var i = 0; i < length; ++i) {
          var rand = Math.floor(Math.random() * ALPHABET.length);
          str += ALPHABET.substring(rand, rand + 1);
        }
        return str;
      }
      ```

      random_str(6) 	返回："NdQKOr"
      上面代码中，random_str函数接受一个整数作为参数，返回变量ALPHABET内的随机字符所组成的指定长度的字符串。

   # Object对象

   **Object的实例方法：**所谓的实例方法就是在定义Object原型对象Object.prototype上的方法。他可以被Object实例直接使用。

   **instanceof**运算符用来验证，一个对象是否为指定的构造函数的实例。

   **Object ( )** 本身是一个函数，可以当作工具方法使用，将任意值转为对象。这个方法常用于保证某个值一定是对象。如果参数为空，（或者为undefined和null），Object（）返回一个空对象。

   属性的描述对象。

   ```javascript
   {
     valeu：123，
     writable：false，
     enumerable：true，
     configurable：false，
     get：undefined，
     set：undefined
   }
   ```

   **属性描述对象提供6个属性；**

   1. `value`
      value是该属性的属性值，默认为undefined。
   2. `writable`
      writable是一个布尔值，表示属性值（value）是否可以改变（即是否可以写），默认是true。
   3. `enumerable`是一个布尔值，表示该属性是否可遍历，默认为true。如果设为false，会使得某些操作（比如for...in循环、Object.keys()）跳过该属性。
   4. `configurable`是一个布尔值，表示可配置性，默认为true。如果设为false，将阻止某些操作改写该属性，比如无法删除该属性，也不得改变该属性的属性描述对象（value属性除外）。
      也就是说，configurable属性控制了属性描述对象的可写性。
   5. `get`
      get是一个函数，表示该属性的取值函数（getter），默认为undefined。
   6. `set`
      set是一个函数，表示该属性的存值函数（setter），默认为undefined。

# Promise对象

1. 什么是Promise。

   Promise 对象是 JavaScript 的异步操作解决方案，为异步操作提供统一接口。它起到代理作用（proxy），充当异步操作与回调函数之间的中介，使得异步操作具备同步操作的接口。Promise 可以让异步操作写起来，就像在写同步操作的流程，而不必一层层地嵌套回调函数。总的来说，Promise就是解决异步操作的解决方法。首先，Promise是一个对象，也是一个构造函数。

   ```javascript
   function f1(resolve, reject) {
     // 异步代码...
   }
   ```

   ```javascript
   var p1 = new Promise(f1)
   ```

   上面代码中，Promise构造函数接受一个回调函数f1作为参数，f1里面是异步操作的代码。然后，返回的p1就是一个 Promise 实例。Promise 的设计思想是，所有异步任务都返回一个 Promise 实例。Promise 实例有一个then方法，用来指定下一步的回调函数。

   ```javascript
   var p1 = new Promise(f1);
   p1.then(f2);
   ```

   上面代码中，f1的异步操作执行完成，就会执行f2。

2. Promise对象的状态

   Promise 对象通过自身的状态，来控制异步操作。Promise 实例具有三种状态。

   1. 异步操作未完成（pending）

   2. 异步操作成功（fulfilled）

   3. 异步操作失败（rejected）

      上面三种状态里面，fulfilled和rejected合在一起称为resolved（已定型）。这三种状态的变化途径只有两种。

      - 从“未完成”到“成功”
      - 从“未完成”到“失败”所以，异步操作，要嘛就是成功，要嘛就是失败。

      如果成功：Promise实例传回一个值（value），状态为fulfilled。
      如果失败：Promise实例抛出一个错误（error），状态为rejected。

3. Promise构造函数

   JavaScript 提供原生的Promise构造函数，用来生成 Promise 实例。

   ```javascript
   var promise = new Promise(function (resolve, reject) {
     // ...
   
     if (/* 异步操作成功 */){
       resolve(value);
     } else { /* 异步操作失败 */
       reject(new Error());
     }
   });
   ```

   上面代码中，Promise构造函数接受一个函数作为参数，该函数的两个参数分别是resolve和reject。它们是两个函数，由 JavaScript 引擎提供，不用自己实现。

   **resolve函数的作用是**，将Promise实例的状态从“未完成”变为“成功”（即从pending变为fulfilled），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去。
   **reject函数的作用是**，将Promise实例的状态从“未完成”变为“失败”（即从pending变为rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。

4. Promise.protoytype.then() `下面的p2中reject为什么要加new关键字？？？？？搞懂以后删除此`

   Promise实例的then方法，用来添加回调函数。
   then方法可以接受两个回调函数，第一个是异步操作成功时（变为fulfilled状态）的回调函数，第二个是异步操作失败（变为rejected）时的回调函数（该参数可以省略）。一旦状态改变，就调用相应的回调函数。

   ```javascript
   var p1 = new Promise(function (resolve, reject) {
     resolve('成功');
   });
   p1.then(console.log, console.error);
   // "成功"，如果p1返回的是成功，那么then调用成功的方法。
   
   var p2 = new Promise(function (resolve, reject) {
     reject(new Error('失败')); // ????
   });
   p2.then(console.log, console.error);
   // Error: 失败，如果p2返回的是失败，则调用失败的方法。
   ```

   

# this关键字

**this**可以用在构造函数之中，表示实例对象。除此之外，this还可以用在别的场合。但是不管事什么场合，this都有一个共同点：他总是返回一个对象。

1. 涵义

   简单来说：this就是属性或方法“当前”所在的对象。

   ```javascript
   var person = {
     name: '张三',
     describe: function () {
       return '姓名：'+ this.name;
     }
   };
   
   person.describe()
   // "姓名：张三"
   ```

   ```javascript
   <input type="text" name="age" size=3 onChange="validate(this, 18, 99);">
   
   function validate(obj, lowval, hival){
     if ((obj.value < lowval) || (obj.value > hival))
       console.log('Invalid Value!');
   }
   ```

   上面代码中，this.name表示name属性所在的那个对象。由于this.name是在describe方法中调用，而describe方法所在的当前对象是person，因此this指向person，this.name就是person.name。
   总结一下，JavaScript 语言之中，一切皆对象，运行环境也是对象，所以函数都是在某个对象之中运行，this就是函数运行时所在的对象（环境）。这本来并不会让用户糊涂，但是 JavaScript 支持运行环境动态切换，也就是说，this的指向是动态的，没有办法事先确定到底指向哪个对象，这才是最让初学者感到困惑的地方。

2. 实质

   this的设计目的就是在函数体内部，指代函数当前的运行环境。

   ```js
   var f = function () {
     console.log(this.x);
   }
   ```

   上面代码中，函数体里面的this.x就是指当前运行环境的x。

3. 使用场合

   - 全局环境使用this，他指的就是顶层对象window。
   - 构造函数，构造函数中的this，指的是实例对象。

4. 避免多层this

   ```js
   var o = {
     f1: function() {
       console.log(this);
       var that = this;
       var f2 = function() {
         console.log(that);
       }();
     }
   }
   
   o.f1()
   // Object
   // Object
   ```

   上面代码定义了变量that，固定指向外层的this，然后在内层使用that，就不会发生this指向的改变。事实上，使用一个变量固定this的值，然后内层函数调用这个变量，是非常常见的做法，请务必掌握。内层的this不能指向外层的对象。而是指向定层的对象。解决方法就是上面的例子。使用一个变量接受this，把当前的this赋值给声明的这个变量。就可以在下层运用这个变量来获取外层的对象了。

5. 绑定this的方法

   javascript提供了 **call**、**apply**、**bind**这三种方法，来切换固定this的指向。

   1.  call（）

      函数实例的call方法，可以指定函数内部this的指向（即函数执行时所在的作用域），然后在所指定的作用域中，调用该函数。call方法的参数，应该是一个对象。如果参数为空、null和undefined，则默认传入全局对象。

      ```javascript
      var n = 123;
      var obj = { n: 456 };
      
      function a() {
        console.log(this.n);
      }
      
      a.call() // 123
      a.call(null) // 123
      a.call(undefined) // 123
      a.call(window) // 123
      a.call(obj) // 456
      ```

      上面代码中，a函数中的this关键字，如果指向全局对象，返回结果为123。如果使用call方法将this关键字指向obj对象，返回结果为456。可以看到，如果call方法没有参数，或者参数为null或undefined，则等同于指向全局对象。

      如果call方法的参数是一个原始值，那么这个原始值会自动转成对应的包装对象，然后传入call方法。

      ```javascript
      var f = function () {
        return this;
      };
      
      f.call(5)
      // Number {[[PrimitiveValue]]: 5}
      ```

      上面代码中，call的参数为5，不是对象，会被自动转成包装对象（Number的实例），绑定f内部的this。
      call的第一个参数就是this所要指向的那个对象，后面的参数则是函数调用时所需的参数。

      ```js
      function add(a, b) {
        return a + b;
      }
      
      add.call(this, 1, 2) // 3
      ```

      上面代码中，call方法指定函数add内部的this绑定当前环境（对象），并且参数为1和2，因此函数add运行后得到3。

      **总的来说**：call方法就是让this绑定到当前的方法中去。

   2. apply（）

      apply方法的第一个参数也是this所要指向的那个对象，如果设为null或undefined，则等同于指定全局对象。第二个参数则是一个数组，该数组的所有成员依次作为参数，传入原函数。原函数的参数，在call方法中必须一个个添加，但是在apply方法中，必须以数组形式添加。

      例：找出数组中最大的元素
      JavaScript 不提供找出数组最大元素的函数。结合使用apply方法和Math.max方法，就可以返回数组的最大元素。

      ```js
      var a = [10, 2, 4, 15, 9];
      Math.max.apply(null, a) // 15
      ```

   3. bind（）

      bind()方法用于将函数体内的this绑定到某个对象，然后返回一个新函数。

      ```javascript
      var d = new Date();
      d.getTime() 
      // 1481869925657
      var print = d.getTime;
      print() 
      // Uncaught TypeError: this is not a Date object.
      ```

      上面代码中，我们将d.getTime()方法赋给变量print，然后调用print()就报错了。这是因为getTime()方法内部的this，绑定Date对象的实例，赋给变量print以后，内部的this已经不指向Date对象的实例了。

      bind()方法可以解决这个问题。

      ```javascript
      var print = d.getTime.bind(d);
      print() 
      // 1481869925657
      ```

      上面代码中，bind()方法将getTime()方法内部的this绑定到d对象，这时就可以安全地将这个方法赋值给其他变量了。

      bind方法的参数就是所要绑定this的对象，下面是一个更清晰的例子。

      ```js
      var counter = {
        count: 0,
        inc: function () {
          this.count++;
        }
      };
      
      var func = counter.inc.bind(counter);
      func();
      counter.count // 1
      ```

      上面代码中，counter.inc()方法被赋值给变量func。这时必须用bind()方法将inc()内部的this，绑定到counter，否则就会出错。

# 定时器

JavaScript 提供定时执行代码的功能，叫做定时器（timer），主要由setTimeout()和setInterval()这两个函数来完成。它们向任务队列添加定时任务。

1. setTimeout（）
   **setTimeout**函数用来指定某个函数或某段代码，在多少毫秒之后执行。它返回一个整数，表示定时器的编号，以后可以用来取消这个定时器。

   ```js
   var timerId = setTimeout(func|code, delay);
   ```

   上面代码中，**setTimeout**函数接受两个参数，第一个参数func|code是将要推迟执行的函数名或者一段代码，第二个参数delay是推迟执行的毫秒数。

2. setInterval（）

   **setInterval**函数的用法与**setTimeout**完全一致，区别仅仅在于setInterval指定某个任务每隔一段时间就执行一次，也就是无限次的定时执行。

   ```js
   var i = 1
   var timer = setInterval(function() {
     console.log(2);
   }, 1000)
   ```

   上面代码中，每隔1000毫秒就输出一个2，会无限运行下去，直到关闭当前窗口。

3. clearTimeout()，clearInterval() 关闭定时器

   **setTimeout**和**setInterval**函数，都返回一个整数值，表示计数器编号。将该整数传入clearTimeout和clearInterval函数，就可以取消对应的定时器。

   ```js
   var id1 = setTimeout(f, 1000);
   var id2 = setInterval(f, 1000);
   
   clearTimeout(id1);
   clearInterval(id2);
   ```

   上面代码中，回调函数f不会再执行了，因为两个定时器都被取消了。

4. debounce函数。（防止抖动）

   防止抖动，意思就是在多少时间内，发生重复的事情可以不触发。比如用户点击键盘，如果用户一直点击，就会造成事件的重复发生。可以让他多少时间，（就是多少秒之后再继续执行一次）

# 函数

1. 概述

   1. javascript有三种方法声明函数。

      

   - function命令声明的代码区块，就是一个函数。function命令后面是函数名，函数名后面是一对圆括号，里面是传入函数的参数。函数体放在大括号里面。

   - ```js
     function print（s）{
     	console.log(s);
     }
     ```

     调用函数：**print()**。函数名加上（）；

2. 变量赋值的写法声明

   ```js
   var print = funtion（s）{
   	console.log（s）;
   }
   ```

   采用函数表达式声明函数时，function命令后面不带有函数名。如果加上函数名，该函数名只在函数体内部有效，在函数体外部无效。
   注：这种表达式声明的函数必须在语句的结尾加上分号，表示语句结束。而上面一种不需要在结尾加分号。

3. 构造函数

   ```js
   var add = function（
   	‘x’,
   	'y',
   	'return  x+y'
   ）;
   ```

   因为这种声明方法不直观，所以用得很少。
   如果一个函数被多次声明，后面的声明会覆盖前面的声明。
   调用函数时，要使用圆括号。里面可以放置参数。

4. 函数的属性和方法

   1. name属性：返回函数的名字。

      如果是通过变量赋值定义的函数，那么，name属性返回的是变量名。**注：只有在变量的值是一个匿名函数的时候才会如此**。在函数中，参数`.name`。就能在控制台打印出当前函数的name。

      匿名函数：例：

      ```js
      var f2 = function （）{
      	f2.name  // name = f2
      }
      ```

      具名函数：例：注意：下面这个函数真正的函数名还是f2，Myname名字只能在函数内部可以用。

      ```js
      var f2 = function Myname（）{
      	f2.name  // name=Myname
      }
      ```

   2. length属性

      函数的length属性返回函数预期传入的参数个数，即函数定义之中的参数个数。不管调用时候传入了多少个参数，length属性值返回创建时小括号中的个数。

   3. toString（）

      toString（）方法，返回一个字符串。

      例：

      var a = 123：此时的a是number数字类型。
      toString（a）；返回一个 “123”

   4. 函数的作用域

      在函数内部声明的变量叫局部变量，在函数外部声明的变量叫全局变量。函数的作用域是在 函数定义时的作用域，而不是在调用时的作用域。

   5. 参数

      函数运行的时候，有时候需要提供外部的数据，不同的外部数据会得到不同的结果。这种外部数据就叫做参数。

      例：

      ```js
      function square （x）{
      	return x*x；
      }
      ```

      square（2）；在调用函数时，传入一个2 作为参数，返回的结果就是2*2=4
      square（3）；返回的结果是9.

   6. arguments

      ```js
      var f = function（a，b）{
      	arguments[ 0 ] = 3;
      	arguments[ 1 ] = 2;
      	return a + a;
      }
      f( 1,1 )
      ```

      上面的代码中，函数 f（）调用时传入的参数，在函数内部被修改成3和2

   7. 闭包

      定义在一个函数内部的函数。特点：就是它可以记住诞生的环境。在本质上，闭包就是将函数别不核函数外部连接起来的一座桥梁。

# 事件的冒泡

事件的冒泡就是点击一个最上面的（z-index 最大）的div。触发事件以后，在他之后的div（z-index 第二个）的事件也会触发。还有最大的一个div（z-index 最小的）事件也会触发

冒泡：事件的向上传导

例：一个span标签上的onclick，触发一个p标签上的onclick，触发一个div上的onclick。。。。。。
切触发的是相同的时间。如，鼠标点击事件，就只冒泡点击事件。如鼠标移动事件就只触发移动事件。

取消冒泡：
属性.cancelBubble = true;

# 数组

数组时按次序排列的一组值。每个值的位置都有编号。编号从0开始。整个数组用方括号表示 ：[ ]。

```js
var arr = [ 'a', 'b,' 'c' ];
```

这就是一个简单数组，数组的a的下标是0。第一位是0，第二位是1，第三位是2.以此类推。所以数组的下标总是比数组的长度小一。数组也是可以先定义、再赋值的。

```js
var arr = [ ];
arr [ 0 ] = 'a';
arr [ 1 ] = 'b';
arr [ 2 ] = 'c';
```

任何类型的数据，都可以放入数组中。比如。函数、对象、方法、数值、字符串、数组里面也能嵌套数组。这时候叫多维数组......

1. 数组的长度

   使用length属性可以返回数组的长度。清空数组可以将length属性设置为0。如果人为设置length大于当前元素个数，则数组的成员数量会增加到这个值，新增的位置都是空位。使用undefined站位。表示空，未定义。

2. 数组的遍历

   数组的遍历可以用for循环、while循环、不建议用for...in循环。常用的是forEach循环。

   ```js
   // for循环
   var a = [ 1, 2, 3 ];
   for ( var i = 0; i < a.length; i ++) {
   	console.log( a[ i ] )；
   	// 打印出a数组的每一项
   }
   ```

   ```js
   // while循环：
   var i = 0；
   while (i < a.length) {
     console.log(a[i]);
     i++;
   }
   ```

   ```js
   // forEeach循环：
   var colors = ['red', 'green', 'blue'];
   colors.forEach(function (color) {
     console.log(color);
   })
   // 打印出colors的每一项。
   ```

3. delete删除

   如果使用delete命令删除数组中的某一项。

   ```js
   var a = [ 1, 2, 3 ];
   delete a[ 1 ]; // 删除a数组的第二个数。
   ```

   此时：a[ 1 ]打印出来的值 = undefined。

   此时：a.length=3

   数组的某个位置是空位、与某个位置是undefined是不一样的，如果是空位，但是对length属性没有影响。所以用length遍历时要小心。如果是空位，使用数组的forEach方法、for...in结构、以及Object.keys方法进行遍历，空位都会被跳过。

   ```js
   var q = ["1","2","3"]
   	q.forEach(function(i,x){
   	console.log(i+"."+x)
   })
   ```

   i代表每一项的值，x代表每一项的下标。

# 高级数组

1. Array.isArray（）方法

   返回一个布尔值。表示参数是否为数组。他可以弥补typeof运算符的不足。说白了，就是用来判断一个参数，或者一个变量是不是数组。

2. valueOf 方法
   valueOf方法是一个所有对象都拥有的方法，表示对该对象求值。不同对象的valueOf方法不尽一致，数组的valueOf方法返回数组的本身。

   ```js
   var arr = [ 1, 2, 3 ];
   arr.valueOf() //控制台输出[ 1, 2, 3 ]
   ```

   返回数组的本身。

3. toString方法

   toString方法也是对象通用的方法，数组的toString方法返回数组的字符串形势。
   例：

   ```js
   var arr = [ 1, 2, 3 ]
   arr.toString() //控制台输出“1,2,3”；
   ```

   就是把数组里面的值都变成一串长的字符串。即使是数组里面有嵌套也是一样的。

4. **数组中的方法**

   1. **push（）**

      push方法用于在数组的末端添加一个或多个元素，并返回添加新元素后的数组长度。注意，该方法会改变原数组。
      例

      ```js
      var arr = [ ];
      arr.push( 1 )
      arr.push( 'a' )
      arr.push( true,{} )
      ```

      此时arr数组里面的值为。【1，‘a’，true，{ }】上面的代码使用push方法，往数组中添加的四个成员。

   2. **pop（）**

      pop方法用于删除数组的最后一个元素，并返回该元素。注意，该方法会改变原数组。

      ```js
      var arr = ['a', 'b', 'c'];
      arr.pop( ) // 'c'
      arr // ['a', 'b']
      ```

      此时在控制台打印输出arr的值为 [ 'a', 'b' ],因为最后一个元素被删除了。**注意**，对空数字使用pop（）不会报错，而是返回一个undefined。

   3. shift（）

      shift( )方法用于删除数组的第一个元素，并返回该元素。注意，该方法会改变原数组。

      ```js
      var a = ['a', 'b', 'c'];
      a.shift() // 删除a中的 'a'
      a // 此时a数组只剩下['b', 'c']
      ```

      只能数组名.shift。然后删除该数组中的第一项。
      shift（）可以遍历清空一个数组。前提是数组的元素不能是0或者任何布尔值等于false的元素，所以，用这个遍历数组不是很可靠。

   4. unshift（）

      unshift( )方法用于在数组的第一个位置添加元素，并返回添加新元素后的数组长度。注意，该方法会改变原数组。unshift（）方法可以接受多个参数，这些参数都会加到目标数组的头部。也就是前面。

   5. join（）

      join( )方法以指定参数作为分隔符，将所有数组成员连接为一个字符串返回。如果不提供参数，默认用逗号分隔。

      ```js
      var a = [1, 2, 3, 4];
      
      a.join(' ') // '1 2 3 4'
      a.join(' | ') // "1 | 2 | 3 | 4"
      a.join() // "1,2,3,4"
      ```

      传入的参数是什么，就会在返回的数组中间加什么。用双引号引起来。如果元素是undefined和null。或者空位，会被转成空字符串。“ ”就是一个空格的样子。

   6. concat（）

      concat方法用于多个数组的合并。它将新数组的成员，添加到原数组成员的后部，然后返回一个新数组，原数组不变。

      ```js
      ['hello'].concat(['world'])
      // ["hello", "world"]
      
      ['hello'].concat(['world'], ['!'])
      // ["hello", "world", "!"]
      
      [].concat({a: 1}, {b: 2})
      // [{ a: 1 }, { b: 2 }]
      
      [2].concat({a: 1})
      // [2, {a: 1}]
      ```

   7. reverse（）

      reverse方法用于颠倒排列数组元素，返回改变后的数组。注意，该方法将改变原数组

      ```js
      var a = ['a', 'b', 'c'];
      
      a.reverse( ) // ["c", "b", "a"]
      a // ["c", "b", "a"]
      ```

      就是第一个在最后一个，最后一个在第一个。颠倒过来了。

   8. slice（）

      sliec（）方法用于提取目标数组的一部分，返回一个新数组，原数组不变。它的第一个参数为起始位置（从0开始，会包括在返回的新数组之中），第二个参数为终止位置（但该位置的元素本身不包括在内）
      如果省略第二个参数，则一直返回到原数组的最后一个成员。

      ```js
      var a = ['a', 'b', 'c'];
      
      a.slice(0) // ["a", "b", "c"]
      a.slice(1) // ["b", "c"]
      a.slice(1, 2) // ["b"]
      a.slice(2, 6) // ["c"]
      a.slice() // ["a", "b", "c"]。
      ```

      截取一个数组中的某元素到某元素的那一段，组成一个新的数组。新的数组包含第一个元素，不包含最后一个元素。且原数组不会改变。如果没有参数。如上面的最后一个例子:则就是拷贝一个与原数组相同的新数组出来。如果给的参数是负数。则表示从后面开始计算。

      ```js
      var a = ['a', 'b', 'c'];
      a.slice(-2) // ["b", "c"]
      a.slice(-2, -1) // ["b"]
      ```

      上面代码中，-2表示倒数计算的第二个位置，-1表示倒数计算的第一个位置。如果第一个参数大于等于数组长度，或者第二个参数小于第一个参数，则返回空数组

   9. **splice（）**

      splice的第一个参数是删除的起始位置（从0开始）第二个参数是被删除的元素个数。如果后面还有更多参数，则表示这些就是要被插入数组的新元素。**注意**，该方法会改变原数组。

      ```js
      var a = ['a', 'b', 'c', 'd', 'e', 'f'];
      a.splice(4, 2) // ["e", "f"]
      a // ["a", "b", "c", "d"]
      ```

      就是删除一个数组里面的元素。第一个参数是下标的位置，第二个参数是删除的个数。从下标是第几个开始删除。

      ```js
      var a = ['a', 'b', 'c', 'd', 'e', 'f'];
      a.splice(4, 2, 1, 2) // ["e", "f"]
      a // ["a", "b", "c", "d", 1, 2]
      ```

      删除以后又加进来两个新元素。如果起始位置是负数，就表示从倒数位置开始删除。

      ```js
      var a = ['a', 'b', 'c', 'd', 'e', 'f'];
      a.splice(-4, 2) // ["c", "d"]
      ```

      倒数第四个开始删除，删除开始以后的前两个元素。所以删除的是【“c”，“d”】
      如果是单纯的插入元素，也可以使用splice（）将第二个参数设置为0，就可以了。这时候，第一个参数表示插入的位置，第三个或者第三个以后的参数就是需要插入的新元素。如果只提供一个参数。就等同于将原数组才拆分为两个数组。从第一个参数的位置起开始拆分。

      例：

      ```js
      var a = [1, 2, 3, 4];
      a.splice(2) // [3, 4]
      a // [1, 2]
      ```

   10. sort（）

       sort方法对数组成员进行排序，默认是按照字典顺序排序。排序后，原数组将被改变。例：

       ```js
       ['d', 'c', 'b', 'a'].sort()
       // ['a', 'b', 'c', 'd']
       
       [4, 3, 2, 1].sort()
       // [1, 2, 3, 4]
       
       [11, 101].sort()
       // [101, 11]
       
       [10111, 1101, 111].sort()
       // [10111, 1101, 111]
       ```

       上面代码的最后两个例子，需要特殊注意。sort()方法不是按照大小排序，而是按照字典顺序。也就是说，数值会被先转成字符串，再按照字典顺序进行比较，所以101排在11的前面。

   11. **map（）**

       map方法将数组的所有成员依次传入参数函数，然后把每一次的执行结果组成一个新数组返回。

       ```js
       var numbers = [1, 2, 3];
       
       numbers.map(function (n) {
         return n + 1;
       });
       // [2, 3, 4]
       
       numbers
       // [1, 2, 3]
       ```

       上面代码中，numbers数组的所有成员依次执行参数函数，运行结果组成一个新数组返回，原数组没有变化。

       map方法接受一个函数作为参数。该函数调用时，map方法向它传入三个参数：当前成员、当前位置和数组本身。

       ```js
       [1, 2, 3].map(function(elem, index, arr) {
         return elem * index;
       });
       // [0, 2, 6]
       ```

       上面代码中，map方法的回调函数有三个参数，elem为当前成员的值，index为当前成员的位置，arr为原数组（[1, 2, 3]）。

   12. **foreach（）**

       forEach的用法与map方法一致，参数是一个函数，该函数同样接受三个参数：当前值、当前位置、整个数组。

       ```js
       function log(element, index, array) {
         console.log('[' + index + '] = ' + element);
       }
       
       [2, 5, 9].forEach(log);
       // [0] = 2
       // [1] = 5
       // [2] = 9
       ```

       上面代码中，forEach遍历数组不是为了得到返回值，而是为了在屏幕输出内容，所以不必使用map方法。**注意**：forEach（）参数是一个方法，方法中的第一个参数是当前数组中的值，第一个值就是第一个值打印出来，第二个参数是当前数组的当前值的下标。第三个参数是整个数组。且记住，大写Each的首字母。

       forEach方法也可以接受第二个参数，绑定参数函数的this变量。

       ```js
       var out = [];
       
       [1, 2, 3].forEach(function(elem) {
         this.push(elem * elem);
       },  out );
       
       out // [1, 4, 9]
       ```

       上面代码中，空数组out是forEach方法的第二个参数，结果，回调函数内部的this关键字就指向out。

       **注意**，forEach方法无法中断执行，总是会将所有成员遍历完，forEach方法也会跳过数组的空位。

   13. **filter（）**

       filter方法用于过滤数组成员，满足条件的成员组成一个新数组返回。它的参数是一个函数，所有数组成员依次执行该函数，返回结果为true的成员组成一个新数组返回。该方法不会改变原数组。

       ```js
       [1, 2, 3, 4, 5].filter(function (elem) {
         return (elem > 3);
       })
       // [4, 5]
       ```

       上面代码将大于3的数组成员，作为一个新数组返回。

       ```js
       var arr = [0, 1, 'a', false];
       
       arr.filter(Boolean)
       // [1, "a"]
       ```

       上面代码中，filter方法返回数组arr里面所有布尔值为true的成员。filter方法的参数函数可以接受三个参数：当前成员，当前位置和整个数组。

       ```js
       [1, 2, 3, 4, 5].filter(function (elem, index, arr) {
         return index % 2 === 0;
       });
       // [1, 3, 5]
       ```

       上面代码返回偶数位置的成员组成的新数组。

       filter方法还可以接受第二个参数，用来绑定参数函数内部的this变量。

       ```js
       var obj = { MAX: 3 };
       var myFilter = function (item) {
         if (item > this.MAX) return true;
       };
       
       var arr = [2, 8, 3, 4, 1, 3, 2, 9];
       arr.filter(myFilter, obj) // [8, 4, 9]
       ```

       上面代码中，过滤器myFilter内部有this变量，它可以被filter方法的第二个参数obj绑定，返回大于3的成员。

   14. some（），every（）

       他们和forEach一样都接受一个函数作为参数。分别是当前成员，当前成员的下标。整个数组。不同是，some（），every（）返回一个布尔值。some方法是只要一个成员的返回值是true，则整个some方法的返回值就是true，否则返回false。

       ```js
       var arr = [1, 2, 3, 4, 5];
       arr.some(function (elem, index, arr) {
         return elem >= 3;
       });
       // true
       ```

       some方法是只要一个成员的返回值是true，则整个some方法的返回值就是true，否则返回false。

       ```js
       var arr = [1, 2, 3, 4, 5];
       arr.every(function (elem, index, arr) {
         return elem >= 3;
       });
       // false
       ```

   15. indexOf（），lastIndexOf（）

       indexOf方法返回给定元素在数组中第一次出现的位置，如果没有出现则返回-1。

       ```js
       var a = ['a', 'b', 'c'];
       
       a.indexOf('b') // 1
       a.indexOf('y') // -1
       ```

       indexOf方法还可以接受第二个参数，表示搜索的开始位置。

       ```js
       ['a', 'b', 'c'].indexOf('a', 1) // -1
       ```

       上面代码从1号位置开始搜索字符a，结果为-1，表示没有搜索到。lastIndexOf方法返回给定元素在数组中最后一次出现的位置，如果没有出现则返回-1。

       ```js
       var a = [2, 5, 9, 2];
       a.lastIndexOf(2) // 3
       a.lastIndexOf(7) // -1
       ```

       注意，这两个方法不能用来搜索NaN的位置，即它们无法确定数组成员是否包含NaN。

# 异步操作的概述

1. 回调函数。

   下面是两个函数f1和f2，编程的意图是f2必须等到f1执行完成，才能执行。

   ```js
   function f1() {
     // ...
   }
   
   function f2() {
     // ...
   }
   
   f1();
   f2();
   ```

   上面代码的问题在于，如果f1是异步操作，f2会立即执行，不会等到f1结束再执行。这时，可以考虑改写f1，把f2写成f1的回调函数。

   ```js
   function f1(callback) {
     // ...
     callback();
   }
   
   function f2() {
     // ...
   }
   
   f1(f2);
   ```

   回调函数的优点是简单、容易理解和实现，缺点是不利于代码的阅读和维护，各个部分之间高度耦合（coupling），使得程序结构混乱、流程难以追踪（尤其是多个回调函数嵌套的情况），而且每个任务只能指定一个回调函数。

# 元素的其他属性

1. clientWidth（获取元素的宽度）
   clientHeight（获取元素的高度）
   这两个属性可以获取元素的可见宽度。获取的值不带px，可以直接计算，包含padding。属性只读，不能修改。
2. offsetWidth和offsetHeigth
   获取元素的整个高度，包括boder，padding。内容。
3. offsetLeft
   当前元素相对于其定位父元素的水平偏移量

4. offsetTop
   当前元素相对于其定位父元素的垂直偏移量

5. scrollLeft
   可以获取水平滚动条滚动的距离
   scrollTop
   可以获取垂直滚动条滚动的距离
   scrollHeight
6. 元素的滚动高度

7. 事件对象，enent获取鼠标当前位置

# 字符串的方法

1. charAt（）

   获取输入字符串指定位置的字符。下标从0开始。

2. charCodeAt（）

   获取指定位置的字符编码。

3. indexof（）

   该方法可以检索一个字符串中是否含有指定的内容。返回，如果字符串中有含有该内容的，则会返回其第一次出现的索引位置。如果没有找到指定的内容，则返回-1，可以指定开始查找的位置。

   ```js
   result = str.indexOf("h",1)
   ```

4. lastIndexOf（）

   方法和indexOf基本一样，一个从前  一个从后。

5. slice（）

   可以从字符串中截取指定的内容，不会影响原来的字符串。而是将截取的字符串返回。参数，第一个，开始位置的索引（包括开始位置）第二个，结束位置的索引（不包括结束位置）第二个参数可以省略，则从第一个开始截取到最后的字符串。

   ```js
   str= “abcdefkjak”
   result = str.slice(1,2)
   result = bc。
   ```

6. substr（）

   从第几个开始截取，截取后面的几个字符。

# 正则表达式

正则表达式（regular expression）是一种表达文本模式（即字符串结构）的方法，有点像字符串的模板，常常用来按照“给定模式”匹配文本。比如，正则表达式给出一个 Email 地址的模式，然后用它来确定一个字符串是否为 Email 地址。

1. 新建一个正则表达式：

   ```js
   var regex = /xyz/；
   ```

   以斜杠表示开始和结束。

   以斜杠表示开始和结束。

2. test（）
   正则实例test（）方法返回一个布尔值，表示当前模式是否能匹配参数字符串。如果能匹配，返回一个true。

3. index：
   模式匹配成功的开始位置。下标从0开始。

4. input：
   整个原字符串。(3、4)例：

   ```js
   var r = /a(b+)a/;
   var arr = r.exec('_abbba_aba_');
   arr // ["abbba", "bbb"]
   
   arr.index // 1
   arr.input // "_abbba_aba_"
   ```

   上面代码中的index属性等于1，是因为从原字符串的第二个位置开始匹配成功。

5. String.prototype.search( )

   字符串对象的search方法，返回第一个满足条件的匹配结果在整个字符串中的位置。如果没有任何匹配，则返回-1。

6. 位置字符
   ^：表示字符串的开始位置。
   $：表示字符串的结束位置。
   例：

   ```js
   // test必须出现在开始位置
   /^test/.test('test123') // true
   // test必须出现在结束位置
   /test$/.test('new test') // true
   
   // 从开始位置到结束位置只有test
   /^test$/.test('test') // true
   /^test$/.test('test test') // false
   ```

7. 选择符（ | ）

   竖线符号（|）在正则表达式中表示“或关系”（OR），即cat|dog表示匹配cat或dog。

   ```js
   /11|22/.test('911') // true
   ```

   上面代码中，正则表达式指定必须匹配11或22。多个选择符可以联合使用。

   ```js
   // 匹配fred、barney、betty之中的一个
   /fred|barney|betty/
   ```

8. 连字符

   某些情况下，对于连续序列的字符，连字符（-）用来提供简写形式，表示字符的连续范围。比如，[abc]可以写成[a-c]，[0123456789]可以写成[0-9]，同理[A-Z]表示26个大写字母。

   ```js
   /a-z/.test('b') // false
   /[a-z]/.test('b') // true
   ```


   上面代码中，当连字号（dash）不出现在方括号之中，就不具备简写的作用，只代表字面的含义，所以不匹配字符b。只有当连字号用在方括号之中，才表示连续的字符序列。

   以下都是合法的字符类简写形式。

   ```js
   [0-9.,]
   [0-9a-fA-F]
   [a-zA-Z0-9-]
   [1-31]
   ```


   上面代码中最后一个字符类[1-31]，不代表1到31，只代表1到3。

   连字符还可以用来指定 Unicode 字符的范围。
   

9. 预定义模式
   预定义模式指的是某些常见模式的简写方式。

   `\d` 匹配0-9之间的任一数字，相当于`[0-9]`。
   `\D` 匹配所有0-9以外的字符，相当于[^0-9]。
   `\w` 匹配任意的字母、数字和下划线，相当于`[A-Za-z0-9_]`。
   `\W` 除所有字母、数字和下划线以外的字符，相当于`[^A-Za-z0-9]`。
   `\s` 匹配空格（包括换行符、制表符、空格符等），相等于`[ \t\r\n\v\f]`。
   `\S` 匹配非空格的字符，相当于`[^ \t\r\n\v\f]`。
   `\b` 匹配词的边界。
   `\B` 匹配非词边界，即在词的内部。
   下面是一些例子。

   ```js
   // \s 的例子
   /\s\w*/.exec('hello world') // [" world"]
   
   // \b 的例子
   /\bworld/.test('hello world') // true
   /\bworld/.test('hello-world') // true
   /\bworld/.test('helloworld') // false
   
   // \B 的例子
   /\Bworld/.test('hello-world') // false
   /\Bworld/.test('helloworld') // true
   ```


   上面代码中，\s表示空格，所以匹配结果会包括空格。\b表示词的边界，所以world的词首必须独立（词尾是否独立未指定），才会匹配。同理，\B表示非词的边界，只有world的词首不独立，才会匹配。

10. 重复类型
    模式的精确匹配次数，使用大括号（{}）表示。{n}表示恰好重复n次，{n,}表示至少重复n次，{n,m}表示重复不少于n次，不多于m次。

    ```js
    /lo{2}k/.test('look') // true
    /lo{2,5}k/.test('looook') // true
    ```


    上面代码中，第一个模式指定o连续出现2次，第二个模式指定o连续出现2次到5次之间。
    

11. 量词符
    ？：问号表示某个模式出现0次或者1次，等同于{0,1}
    *：星好表示某个模式出现0次或者多次，等同于{0，}
    +：加号表示某个模式出现1次或者多次，等同于{1，}

    量词：
     reg = /(ab){3}/  表示ab出现3次
     reg = /b{3}/  表示b出现3次
     reg = /ab{1，3}c/  表示a和c中间的b出现至少一次或3次。
     reg = /ab{3, }c/ 表示a和c中间的b出现3次，或3次以上。

# js后半部部分

[学习地址](https://www.bilibili.com/video/BV1p4411u7TT?p=114)