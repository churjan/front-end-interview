# Javascript问题

## 目录

* [js中有多少个内置类型](#js中有多少个内置类型)
* [什么是闭包](#什么是闭包)
* [什么是作用域,什么是作用域链](#什么是作用域什么是作用域链)
* [函数中的this指向什么](#函数中的this指向什么)
* [js bind 实现机制](#js-bind-实现机制)
* [事件流三个阶段](#事件流三个阶段)
* [简述同步与异步的区别](#简述同步与异步的区别)
* [js中的`new()`到底做了些什么](#js中的new到底做了些什么)
* [对象的几种创建方式](#对象的几种创建方式)
* [继承的6种方法](#继承的6种方法)
* [跨域的几种方式](#跨域的几种方式)
* [手写移动端字体自适应方案](#手写移动端字体自适应方案)
* [什么是原型](#什么是原型)
* [什么是原型链](#什么是原型链)
* [请简述AJAX及基本步骤](#请简述ajax及基本步骤)

### js中有多少个内置类型

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

类型判断终极方法 `Object.prototype.toString`

[[↑] Back to top](#javascript问题)

### 什么是闭包

闭包定义：在函数里面定义一个函数，改子函数可以访问父函数的局部变量。

[[↑] Back to top](#javascript问题)

### 什么是作用域,什么是作用域链

作用域表示的是变量或函数的可访问范围。

它是指对某一变量和方法具有访问权限的代码空间，表示变量或函数起作用的区域，指代了它们在什么样的上下文中执行，亦即上下文执行环境。每个执行环境都有一个与之关联的变量对象(variable object),环境中定义的所有变量和函数都保存在这个对象中。Javascript的作用域只有两种：全局作用域和本地作用域，本地作用域是按照函数来区分的。

当代码在一个环境中执行时,会创建变量对象的一个作用域链(scope chain)。作用域链的用途,是 保证对执行环境有权访问的所有变量和函数的有序访问。作用域链的前端,始终都是当前执行的代码所在环境的变量对象。如果这个环境是函数,则将其活动对象(activation object)作为变量对象。活动对象在最开始时只包含一个变量,即arguments对象(这个对象在全局环境中是不存在的)。作用域链中的下一个变量对象来自包含(外部)环境,而再下一个变量对象则来自下一个包含环境。这样,一直延续到全局执行环境;全局执行环境的变量对象始终都是作用域链中的最后一个对象。

[[↑] Back to top](#javascript问题)

### 函数中的this指向什么

this引用的是函数执行的环境对象

[试题测试](https://juejin.im/post/59aa71d56fb9a0248d24fae3)

[[↑] Back to top](#javascript问题)

### js bind 实现机制

```js
Function.prototype.emulateBind = function(context) {
    let aArgs = Array.prototype.slice.call(arguments, 1); //拿到除了context之外的预置参数序列
    let that = this; //保存this，即调用bind方法的目标函数
    return function() {
        return that.apply(context, aArgs.concat(Array.prototype.slice.call(arguments)))
        //绑定this同时将调用时传递的序列和预置序列进行合并
    }
}

//引用
function a(){
  console.log(this.id);
}
b={id:'b'};
let _a=a.bind(b);
```

参考：  
[http://blog.csdn.net/qq_40479190/article/details/78324282#t1](http://blog.csdn.net/qq_40479190/article/details/78324282#t1)

[[↑] Back to top](#javascript问题)

### 事件流三个阶段

1. 事件捕捉阶段：事件开始由顶层对象触发，然后逐级向下传播，直到目标的元素；
2. 处于目标阶段：处在绑定事件的元素上；
3. 事件冒泡阶段：事件由具体的元素先接收，然后逐级向上传播，直到不具体的元素；

[[↑] Back to top](#javascript问题)

### 简述同步与异步的区别

同步是阻塞模式，异步是非阻塞模式。

同步就是指一个进程在执行某个请求的时候，若该请求需要一段时间才能返回信息，那么这个进程将会一直等待下去，直到收到返回信息才继续执行下去;

异步是指进程不需要一直等下去，而是继续执行下面的操作，不管其他进程的状态。当有消息返回时系统会通知进程进行处理，这样可以提高执行的效率。

参考：  
[http://www.ruanyifeng.com/blog/2014/10/event-loop.html](http://www.ruanyifeng.com/blog/2014/10/event-loop.html)

[[↑] Back to top](#javascript问题)

### js中的`new()`到底做了些什么

1. 创建一个新的空对象
1. 将this绑定到该对象
1. 添加一个名为__proto__的新属性，并且指向构造函数的原型(prototype)
1. 返回该this对象

```js
var obj  = {};
obj.__proto__ = Base.prototype;
Base.call(obj);
```

参考：https://juejin.im/post/59eb1dee6fb9a0450e75427e

[[↑] Back to top](#javascript问题)

### 对象的几种创建方式

1. 工厂模式
1. 构造函数模式
1. 原型模式
1. 混合构造函数和原型模式
1. 动态原型模式
1. 寄生构造函数模式
1. 稳妥构造函数模式

参考：红宝书 6.2 创建对象

[[↑] Back to top](#javascript问题)

### 继承的6种方法

1. 原型链继承
1. 借用构造函数继承
1. 组合继承(原型+借用构造)
1. 原型式继承
1. 寄生式继承
1. 寄生组合式继承

参考：红宝书 6.3 继承

[[↑] Back to top](#javascript问题)

### 跨域的几种方式

首先了解下浏览器的同源策略

同源策略/SOP（Same origin policy）是一种约定，由Netscape公司1995年引入浏览器，它是浏览器最核心也最基本的安全功能，如果缺少了同源策略，浏览器很容易受到XSS、CSFR等攻击。所谓同源是指"协议+域名+端口"三者相同，即便两个不同的域名指向同一个ip地址，也非同源。

那么怎样解决跨域问题的呢

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

参考：  
[https://segmentfault.com/a/1190000011145364](https://segmentfault.com/a/1190000011145364)

[[↑] Back to top](#javascript问题)

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

### 什么是原型

每创建一个函数，函数上都有一个属性为prototype，它的值是一个对象。这个对象的作用在于当使用函数创建实例的时候，那么这些实例都会共享这个对象上的属性和方法。

[[↑] Back to top](#javascript问题)

### 什么是原型链

在JavaScript中，每个对象都有一个指向它的原型（prototype）对象的内部链接（proto）。这个原型对象又有自己的原型，直到某个对象的原型为null为止（也就是不再有原型指向）。这种一级一级的链结构就称为原型链（prototype chain）。当查找一个对象的属性时，JavaScript会向上遍历原型链，直到找到给定名称的属性为止;到查找到达原型链的顶部（Object.prototype），仍然没有找到指定的属性，就会返回undefined。

[[↑] Back to top](#javascript问题)

### 请简述AJAX及基本步骤

```js
function makeRequest(url) {
  let xhr = new XMLHttpRequest();
  xhr.open('GET', url, true);
  xhr.send(null);
  xhr.onreadystatechange = function () {
      if (xhr.readyState == 4) {
          if(xhr.status==200){
              let res=JSON.parse(xhr.responseText);
          }else{
              alert('err');
          }
      }
  };
}
makeRequest(url);
```

[[↑] Back to top](#javascript问题)
