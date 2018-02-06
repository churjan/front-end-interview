# 前端面试题目

## <div id="catalog">目录</div>

1. [开放性问题](#base)
1. [HTML部分](#html)
1. [CSS部分](#css)
1. [JS概念部分](#js)
1. [JS编程部分](#js2)

## [[⬆]](#catalog) <a name="base">开放性问题</a>  
* 自我介绍：除了基本个人信息以外，面试官更想听的是你与众不同的地方和你的优势。

* 项目介绍

* 如何看待前端开发？

* 平时是如何学习前端开发的？

* 未来三到五年的规划是怎样的？

## [[⬆]](#catalog) <span id="html">HTML部分</span>  
## [[⬆]](#catalog) <span id="css">CSS部分</span>  
## [[⬆]](#catalog) <span id="js">JS概念部分</span>


* js中五大基本（原始）数据类型？  
number,string,boolean,null,underfined
![](https://images2015.cnblogs.com/blog/315302/201702/315302-20170205164840214-221836365.png)

* js中的new()到底做了些什么？
  * 创建一个空对象
  * 将这个空对象的__proto__，指向构造函数的prototype属性
  * 将这个空对象赋值给函数内部的this关键字
  * 开始执行构造函数内部的代码
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
* 什么是闭包，为什么要使用它？  
闭包是指有权访问另一个函数作用域中变量的函数  
闭包可以用在许多地方。它的最大用处有两个，一个是前面提到的可以读取函数内部的变量，另一个就是让这些变量的值始终保持在内存中。  

## [[⬆]](#catalog) <span id="js2">JS编程部分</span>

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




