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



## <div id="js">[:top:](#catalog) JS概念部分</div>



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
