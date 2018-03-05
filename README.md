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
