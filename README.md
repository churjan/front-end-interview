# 前端面试题目

## <div id="catalog">目录</div>

1. [开放性问题](#base)
1. [HTML部分](#html)
1. [CSS部分](#css)
1. [JS概念部分](#js)
1. [JS编程部分](#js2)

## :top:(#catalog) <span id="base">开放性问题</span>  
* 自我介绍：除了基本个人信息以外，面试官更想听的是你与众不同的地方和你的优势。

* 项目介绍

* 如何看待前端开发？

* 平时是如何学习前端开发的？

* 未来三到五年的规划是怎样的？

## :top:(#catalog) <span id="html">HTML部分</span>

## :top:(#catalog) <span id="css">CSS部分</span>

* 什么是BFC?如何触发BFC?

BFC全称为block formatting context,中文为“块级格式化上下文”。具有 BFC特性的元素可以看作是隔离了的独立容器，容器里面的元素不会在布局上影响到外面的元素，并且BFC具有普通容器所没有的一些特性。

触发 BFC

1. `<HTML>`根元素
1. 浮动元素：float 除 none 以外的值
1. position 的值不为 relative 和 static
1. display 为 inline-block、table-cells、flex
1. overflow 除了 visible 以外的值 (hidden、auto、scroll)

## :top:(#catalog) <span id="js">JS概念部分</span>

* js中有多少个内置类型？

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

* 什么是闭包(closure)，为什么要使用它？

闭包就是能够读取其他函数内部变量的函数。
闭包可以用在许多地方。它的最大用处有两个，一个是前面提到的可以读取函数内部的变量，另一个就是让这些变量的值始终保持在内存中。

* 什么是作用域？

它是指对某一变量和方法具有访问权限的代码空间，表示变量或函数起作用的区域，指代了它们在什么样的上下文中执行，亦即上下文执行环境。每个执行环境都有一个与之关联的变量对象(variable object),环境中定义的所有变量和函数都保存在这个对象中。Javascript的作用域只有两种：全局作用域和本地作用域，本地作用域是按照函数来区分的。

* 什么是作用域链？  

当代码在一个环境中执行时,会创建变量对象的一个作用域链(scope chain)。作用域链的用途,是 保证对执行环境有权访问的所有变量和函数的有序访问。作用域链的前端,始终都是当前执行的代码所在环境的变量对象。如果这个环境是函数,则将其活动对象(activation object)作为变量对象。活动对象在最开始时只包含一个变量,即arguments对象(这个对象在全局环境中是不存在的)。作用域链中的下一个变量对象来自包含(外部)环境,而再下一个变量对象则来自下一个包含环境。这样,一直延续到全局执行环境;全局执行环境的变量对象始终都是作用域链中的最后一个对象。

* 事件流三个阶段
1. 事件捕捉阶段：事件开始由顶层对象触发，然后逐级向下传播，直到目标的元素；
1. 处于目标阶段：处在绑定事件的元素上；
1. 事件冒泡阶段：事件由具体的元素先接收，然后逐级向上传播，直到不具体的元素；

* js中的new()到底做了些什么？
  * 创建一个新对象
  * 将构造函数的作用域赋给新对象(因此 this 就指向了这个新对象)
  * 添加一个名为__proto__的新属性，并且指向构造函数的原型(prototype)
  * 执行构造函数中的代码(为这个新对象添加属性)
  * 返回新对象

```js
var obj  = {};
obj.__proto__ = Base.prototype;
Base.call(obj);
```

* 手写移动端字体自适应方案

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

* 什么是原型？  
每创建一个函数，函数上都有一个属性为 prototype，它的值是一个对象。 这个对象的作用在于当使用函数创建实例的时候，那么这些实例都会共享原型上的属性和方法。

* 什么是原型链？  
在 JavaScript 中，每个对象都有一个指向它的原型（prototype）对象的内部链接（proto）。这个原型对象又有自己的原型，直到某个对象的原型为 null 为止（也就是不再有原型指向）。这种一级一级的链结构就称为原型链（prototype chain）。 当查找一个对象的属性时，JavaScript 会向上遍历原型链，直到找到给定名称的属性为止;到查找到达原型链的顶部（Object.prototype），仍然没有找到指定的属性，就会返回 undefined。

* 请简述 AJAX 及基本步骤？  
1. 初始化ajax对象
1. 连接地址，准备数据
1. 发送请求
1. 接收数据（正在接收，尚未完成）
1. 接收数据完成

```js
//初始化ajax对象
var xhr = new XMLHttpRequest();
//连接地址，准备数据
xhr.open(“方式”,”地址”,是否为异步);
//接收数据完成触发的事件
xhr.onload =function(){}
//发送数据
xhr.send();
```


* HTTP 状态消息 200 302 304 403 404 500 分别表示什么？  
1. 200：请求已成功，请求所希望的响应头或数据体将随此响应返回。
1. 302：请求的资源临时从不同的 URI 响应请求。由于这样的重定向是临时的，客户端应当继续向原有地址发送以后的请求。只有在 Cache-Control 或 Expires 中进行了指定的情况下，这个响应才是可缓存的。
1. 304：如果客户端发送了一个带条件的 GET 请求且该请求已被允许，而文档的内容（自上次访问以来或者根据请求的条件）并没有改变，则服务器应当返回这个状态码。304 响应禁止包含消息体，因此始终以消息头后的第一个空行结尾。
1. 403：服务器已经理解请求，但是拒绝执行它。
1. 404：请求失败，请求所希望得到的资源未被在服务器上发现。
1. 500：服务器遇到了一个未曾预料的状况，导致了它无法完成对请求的处理。一般来说，这个问题都会在服务器端的源代码出现错误时出现。

## :top:(#catalog) <span id="js2">JS编程部分</span>

* 考察JS变量声明、作用域、原型链
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

* 实现一个函数 clone()，可以对 JavaScript 中的5种主要的数据类型（包括 Number、String、Object、Array、Boolean）进行值复制。

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
    return o;
}
```




