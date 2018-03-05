# 前端面试题目

纸上得来终觉浅，绝知此事要躬行,骚年们加油:muscle:

## 目录

1. [开放性问题](#base)
1. [HTML,HTTP部分](#html)
1. [CSS部分](#css)
1. [JS概念部分](#js)
1. [Vue部分](#vue)
1. [JS编程部分](#code)

## <div id="base">[:top:](#catalog) 开放性问题</div>

### 自我介绍

### 项目介绍

### 如何看待前端开发？

### 平时是如何学习前端开发的？

### 未来三到五年的规划是怎样的？

## <div id="html">[:top:](#catalog) HTML,HTTP部分</div>

## <div id="css">[:top:](#catalog) CSS部分</div>

### 如何垂直居中一个元素？

有以下HTML标签，假设`父标签宽400px，高200px，子标签宽200px，高100px，`请列出各种垂直居中方法

```html
<div class="father">
    <div class="son"></div>
</div>
```

1.利用`line-height`实现垂直居中

```css
.son{
    line-height:200px;
}
```

2.利用`display: table`实现垂直居中

```css
.father{
    display:table;
    .son{
        display:table-cell;
        vertical-align:center;
    }
}
```

3.`margin`填充

```css
.son{
    margin-top:calc((400px-200px)/2);
}
```

4.经典`absolute`布局上下文垂直居中

```css
.son{
    position:absolute;
    left:50%;
    top:50%;
    margin-left:-100px;
    margin-top:-50px;
}
```

4.CSS3下`absolute`布局上下文垂直居中

```css
.son{
    position:absolute;
    left:50%;
    top:50%;
    transform: translate(-50%,-50%);
}
```

5.利用`margin：auto`居中

```css
.son{
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    width:200px;
    height:100px;
    margin:auto;
}
```

6.利用Flex布局居中

```css
.father{
    display:flex;
    align-items:center;
    justify-content:center;
}
```

参考：[垂直居中实现方式总结](https://juejin.im/entry/58296b1a570c3500587bb553)

### 字体font-family

```text
@ 宋体      SimSun
@ 黑体      SimHei
@ 微信雅黑   Microsoft Yahei
@ 微软正黑体 Microsoft JhengHei
@ 新宋体    NSimSun
@ 新细明体  MingLiU
@ 细明体    MingLiU
@ 标楷体    DFKai-SB
@ 仿宋     FangSong
@ 楷体     KaiTi
@ 仿宋_GB2312  FangSong_GB2312
@ 楷体_GB2312  KaiTi_GB2312  
@
@ 说明：中文字体多数使用宋体、雅黑，英文用Helvetica
body { font-family: Microsoft Yahei,SimSun,Helvetica; }
```

### 什么是BFC？如何触发BFC？

BFC全称为block formatting context,中文为“块级格式化上下文”。具有 BFC特性的元素可以看作是隔离了的独立容器，容器里面的元素不会在布局上影响到外面的元素，并且BFC具有普通容器所没有的一些特性。

触发 BFC

1. `<HTML>`根元素
1. 浮动元素：float 除 none 以外的值
1. position 的值不为 relative 和 static
1. display 为 inline-block、table-cells、flex
1. overflow 除了 visible 以外的值 (hidden、auto、scroll)

### 请写出圣杯布局和双飞翼布局

参考：[圣杯和双飞翼布局介绍](https://segmentfault.com/a/1190000013301463)

## <div id="js">[:top:](#catalog) JS概念部分</div>

### js中有多少个内置类型？

number,string,boolean,null,underfined,symbol(es6新增),object  
除对象之外,其他统称为“基本类型”。

typeof 运算符来查看值的类型,它返回的是类型的字符串值。

```js
typeof 42 //number
typeof '42' //string
typeof true //bollean
typeof null //object
typeof undefined //undefined
typeof Symbol() //symbol
typeof {n:42} //object
typeof function a(){} //function
```

### 什么是闭包(closure)，为什么要使用它？

闭包就是能够读取其他函数内部变量的函数。
闭包可以用在许多地方。它的最大用处有两个，一个是前面提到的可以读取函数内部的变量，另一个就是让这些变量的值始终保持在内存中。

### 什么是作用域？什么是作用域链？

作用域表示的是变量或函数的可访问范围。

它是指对某一变量和方法具有访问权限的代码空间，表示变量或函数起作用的区域，指代了它们在什么样的上下文中执行，亦即上下文执行环境。每个执行环境都有一个与之关联的变量对象(variable object),环境中定义的所有变量和函数都保存在这个对象中。Javascript的作用域只有两种：全局作用域和本地作用域，本地作用域是按照函数来区分的。

当代码在一个环境中执行时,会创建变量对象的一个作用域链(scope chain)。作用域链的用途,是 保证对执行环境有权访问的所有变量和函数的有序访问。作用域链的前端,始终都是当前执行的代码所在环境的变量对象。如果这个环境是函数,则将其活动对象(activation object)作为变量对象。活动对象在最开始时只包含一个变量,即arguments对象(这个对象在全局环境中是不存在的)。作用域链中的下一个变量对象来自包含(外部)环境,而再下一个变量对象则来自下一个包含环境。这样,一直延续到全局执行环境;全局执行环境的变量对象始终都是作用域链中的最后一个对象。

### 函数中的This指向什么？

this引用的是函数执行的环境对象

[试题测试](https://juejin.im/post/59aa71d56fb9a0248d24fae3)

### 事件流三个阶段

1. 事件捕捉阶段：事件开始由顶层对象触发，然后逐级向下传播，直到目标的元素；
1. 处于目标阶段：处在绑定事件的元素上；
1. 事件冒泡阶段：事件由具体的元素先接收，然后逐级向上传播，直到不具体的元素；

### 简述同步与异步的区别

同步是阻塞模式，异步是非阻塞模式。

同步就是指一个进程在执行某个请求的时候，若该请求需要一段时间才能返回信息，那么这个进程将会一直等待下去，直到收到返回信息才继续执行下去;

异步是指进程不需要一直等下去，而是继续执行下面的操作，不管其他进程的状态。当有消息返回时系统会通知进程进行处理，这样可以提高执行的效率。

### js中的new()到底做了些什么？

1. 创建一个新对象
1. 将构造函数的作用域赋给新对象(因此 this 就指向了这个新对象)
1. 添加一个名为__proto__的新属性，并且指向构造函数的原型(prototype)
1. 执行构造函数中的代码(为这个新对象添加属性)
1. 返回新对象

```js
var obj  = {};
obj.__proto__ = Base.prototype;
Base.call(obj);
```

### 对象的几种创建方式

1. 工厂模式
1. 构造函数模式
1. 原型模式
1. 混合构造函数和原型模式
1. 动态原型模式
1. 寄生构造函数模式
1. 稳妥构造函数模式

参考：红宝书 6.2 创建对象

### 继承的6种方法

1. 原型链继承
1. 借用构造函数继承
1. 组合继承(原型+借用构造)
1. 原型式继承
1. 寄生式继承
1. 寄生组合式继承

参考：红宝书 6.3 继承

### 跨域的几种方式

首先了解下浏览器的同源策略

同源策略/SOP（Same origin policy）是一种约定，由Netscape公司1995年引入浏览器，它是浏览器最核心也最基本的安全功能，如果缺少了同源策略，浏览器很容易受到XSS、CSFR等攻击。所谓同源是指"协议+域名+端口"三者相同，即便两个不同的域名指向同一个ip地址，也非同源。

那么怎样解决跨域问题的呢？

1.通过jsonp跨域

```html
<script>
var script = document.createElement('script');
script.type = 'text/javascript';

// 传参并指定回调执行函数为onBack
script.src = 'http://www.....:8080/login?user=admin&callback=onBack';
document.head.appendChild(script);

// 回调执行函数
function onBack(res) {
    alert(JSON.stringify(res));
}
</script>
```

2.document.domain + iframe跨域  

此方案仅限主域相同，子域不同的跨域应用场景。

```html
<!-- 父窗口：(http://www.domain.com/a.html) -->
<iframe id="iframe" src="http://child.domain.com/b.html"></iframe>
<script>
    document.domain = 'domain.com';
    var user = 'admin';
</script>
<!-- 子窗口：(http://child.domain.com/b.html) -->
<script>
    document.domain = 'domain.com';
    // 获取父窗口中变量
    alert('get js data from parent ---> ' + window.parent.user);
</script>
```

3.nginx代理跨域

4.nodejs中间件代理跨域

5.后端在头部信息里面设置安全域名

参考：[更多跨域的具体内容请看](https://segmentfault.com/a/1190000011145364)

### 手写移动端字体自适应方案

```js
 (function (doc, win) {
    var docEl = doc.documentElement,
      resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
      recalc = function () {
        var clientWidth = docEl.clientWidth;
        if (!clientWidth) return;
        var fontSize = 100 * (clientWidth / 750);
        docEl.style.fontSize = fontSize + 'px';
      };
    if (!doc.addEventListener) return;
    win.addEventListener(resizeEvt, recalc, false);
    doc.addEventListener('DOMContentLoaded', recalc, false);
  })(document, window);
```

### 什么是原型？

每创建一个函数，函数上都有一个属性为prototype，它的值是一个对象。这个对象的作用在于当使用函数创建实例的时候，那么这些实例都会共享这个对象上的属性和方法。

### 什么是原型链？

在JavaScript中，每个对象都有一个指向它的原型（prototype）对象的内部链接（proto）。这个原型对象又有自己的原型，直到某个对象的原型为null为止（也就是不再有原型指向）。这种一级一级的链结构就称为原型链（prototype chain）。当查找一个对象的属性时，JavaScript会向上遍历原型链，直到找到给定名称的属性为止;到查找到达原型链的顶部（Object.prototype），仍然没有找到指定的属性，就会返回undefined。

### js bind 实现机制？

```js
Function.prototype.bind = function(context) {
    var aArgs   = Array.prototype.slice.call(arguments, 1) //拿到除了context之外的预置参数序列
    var that = this
    return function() {
        return that.apply(context, aArgs.concat(Array.prototype.slice.call(arguments)))
        //绑定this同时将调用时传递的序列和预置序列进行合并
    }
}
```

参考：  
[手写一个bind](http://blog.csdn.net/qq_40479190/article/details/78324282#t1)

### 请简述AJAX及基本步骤？

1. 初始化ajax对象
1. 连接地址，准备数据
1. 接收数据（正在接收，尚未完成）
1. 发送请求

```js
//初始化ajax对象
var xhr = new XMLHttpRequest();
//连接地址，准备数据
xhr.open(“方式”,”地址”,是否为异步);
//接收数据完成触发的事件
xhr.onreadystatechange =function(){
    if(xhr.readyState===4&&xhr.status===200){
    console.log(xhr.responseText)
    }
}
//发送数据
xhr.send();
```

## <div id="vue">[:top:](#catalog) Vue部分</div>

### 请详细说下你对vue生命周期的理解？

答：总共分为8个阶段创建前/后，载入前/后，更新前/后，销毁前/后。

创建前/后： 在beforeCreated阶段，vue实例的挂载元素$el和数据对象data都为undefined，还未初始化。在created阶段，vue实例的数据对象data有了，$el还没有。

载入前/后：在beforeMount阶段，vue实例的$el和data都初始化了，但还是挂载之前为虚拟的dom节点，data.message还未替换。在mounted阶段，vue实例挂载完成，data.message成功渲染。

更新前/后：当data变化时，会触发beforeUpdate和updated方法。

销毁前/后：在执行destroy方法后，对data的改变不会再触发周期函数，说明此时vue实例已经解除了事件监听以及和dom的绑定，但是dom结构依然存在

### 组件间通信

```text
//1、父传子 （props down）
    //1.父组件 发送
        <son myName='zhangsan'>
        </son>
    //2.子组件 接受
        到son组件：
        Vue.component('son',{
          props:['myName'],
          template:`
           <p>{{myName}}</p>
          `
        })
//2、子与父通信 (events up)
    //1.父组件 绑定
    methods:{
     handleEvent:function(msg){}
    }
    <son @customEvent="handleEvent"></son>
    //2.子组件 触发
    //子组件内部：
    this.$emit(‘customEvent’,100);

//3、ref(reference 引用/参考 外号)
//帮助在父组件中 得到子组件中的数据、方法。
    //1.指定ref属性
    <son ref="mySon"></son>
    //2.根据ref得到子组件实例
    this.$refs.mySon

//4、$parent
    this.$parent得到父组件的实例

//5、兄弟组件通信
    //1.new一个实例
    var bus = new Vue();
    //2.接收方
    bus.$on('eventName',function(msg){})
    //3.发送方
    bus.$emit('eventName',123);
```

### 说下你对mvvm的理解？双向绑定的理解？

mvvm就是vm框架视图、m模型就是用来定义驱动的数据、v经过数据改变后的html、vm就是用来实现双向绑定
双向绑定:一个变了另外一个跟着变了，例如：视图一个绑定了模型的节点有变化，模型对应的值会跟着变

### vue-router有哪几种导航钩子？

三种，
第一种：是全局导航钩子：`router.beforeEach(to,from,next)`，作用：跳转前进行判断拦截。
第二种：组件内的钩子
第三种：单独路由独享组件

### Vue如何实现双向绑定？

原理：通过`Object.defineProperty`实现

```html
<body>
<div id="app">
    <input type="text" id="txt">
    <p id="show-txt"></p>
</div>
<script>
    var obj = {}
    Object.defineProperty(obj, 'txt', {
        get: function () {
            return obj
        },
        set: function (newValue) {
            document.getElementById('txt').value = newValue
            document.getElementById('show-txt').innerHTML = newValue
        }
    })
    document.addEventListener('keyup', function (e) {
        obj.txt = e.target.value
    })
</script>
</body>
```

## <div id="code">[:top:](#catalog) JS编程部分</div>

### 考察JS变量声明、作用域、原型链

```js
function Foo() {
    getName = function () {
        console.log('1');
    };
    return this;
}
Foo.getName = function () {
    console.log('2');
};
Foo.prototype.getName = function () {
    console.log('3');
};
var getName = function () {
    console.log('4');
};
function getName() {
    console.log(5);
}

Foo.getName();
getName();
Foo().getName();
getName();
new Foo.getName();
new Foo().getName();
new new Foo().getName();

请问上述代码在浏览器环境下，输出结果是多少？
```

参考答案：[一道颇有难度的JavaScript题](https://cnodejs.org/topic/5867d50d5eac96bb04d3e302)

### 实现一个函数 clone()，可以对 JavaScript 中的5种主要的数据类型（包括 Number、String、Object、Array、Boolean）进行值复制。

```js
function clone(obj) {
    //判断是对象，就进行循环复制
    if (typeof obj === 'object' && typeof obj !== 'null') {
        // 区分是数组还是对象，创建空的数组或对象
        var o = Object.prototype.toString.call(obj).slice(8, -1) === "Array" ? [] : {};
        for (var k in obj) {
            // 如果属性对应的值为对象，则递归复制
            if(typeof obj[k] === 'object' && typeof obj[k] !== 'null'){
                o[k] = clone(obj[k])
            }else{
                o[k] = obj[k];
            }
        }
    }else{ //不为对象，直接把值返回
        return obj;
    }
}
```

### 统计字符串中字母个数或统计最多字母

```js
var str = "aaaabbbccccddfgh";
var obj  = {};
for(var i=0;i<str.length;i++){
    var v = str.charAt(i);
    if(obj[v]){
        obj[v].count++;
    }else{
        obj[v] = {};
        obj[v].count = 1;
        obj[v].value = v;
    }
}
for(key in obj){
    document.write(obj[key].value +'='+obj[key].count+'&nbsp;'); // a=4  b=3  c=4  d=2  f=1  g=1  h=1
}
```

### 封装一个函数，参数是定时器的时间，.then执行回调函数。

```js
function sleep (time) {

  return new Promise((resolve) => setTimeout(resolve, time));

}
```
