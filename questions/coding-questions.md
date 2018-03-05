# Coding问题

## 目录

* [考察JS变量声明 作用域 原型链](#考察js变量声明-作用域-原型链)
* [深拷贝](#深拷贝)
* [统计字符串中字母个数或统计最多字母](#统计字符串中字母个数或统计最多字母)
* [封装一个函数，参数是定时器的时间，`.then`执行回调函数](#封装一个函数，参数是定时器的时间，then执行回调函数)

### 考察JS变量声明 作用域 原型链

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

请问上述代码在浏览器环境下，输出结果是多少
```

参考答案：[一道颇有难度的JavaScript题](https://cnodejs.org/topic/5867d50d5eac96bb04d3e302)

[[↑] Back to top](#coding问题)

### 深拷贝

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

[[↑] Back to top](#coding问题)

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

[[↑] Back to top](#coding问题)

### 封装一个函数，参数是定时器的时间，`.then`执行回调函数

```js
function sleep (time) {

  return new Promise((resolve) => setTimeout(resolve, time));

}
```
[[↑] Back to top](#coding问题)