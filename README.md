# 前端面试题目

## <a name="catalog">目录</a>

1. [HTML相关问题](#html)
1. [CSS相关问题](#css)
1. [JS相关问题](#js)

## [[⬆]](#catalog) <a name="html">HTML相关问题</a>
  
## [[⬆]](#catalog) <a name="css">CSS相关问题</a>

## [[⬆]](#catalog) <a name="js">JS相关问题</a>

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
闭包就是能够读取其他函数内部变量的函数。  
闭包可以用在许多地方。它的最大用处有两个，一个是前面提到的可以读取函数内部的变量，另一个就是让这些变量的值始终保持在内存中。  





