# Vue问题

## 目录

* [请详细说下你对vue生命周期的理解](#请详细说下你对vue生命周期的理解)
* [组件间通信](#组件间通信)
* [说下你对mvvm的理解，双向绑定的理解](#说下你对mvvm的理解，双向绑定的理解)
* [Vue如何实现双向绑定](#vue如何实现双向绑定)

### 请详细说下你对vue生命周期的理解

答：总共分为8个阶段创建前/后，载入前/后，更新前/后，销毁前/后。

创建前/后： 在beforeCreat阶段，vue实例的挂载元素$el和数据对象data都为undefined，还未初始化。在created阶段，vue实例的数据对象data有了，$el还没有。

载入前/后：在beforeMount阶段，vue实例的$el和data都初始化了，但还是挂载之前为虚拟的dom节点，data.message还未替换。在mounted阶段，vue实例挂载完成，data.message成功渲染。

更新前/后：当data变化时，会触发beforeUpdate和updated方法。

销毁前/后：在执行destroy方法后，对data的改变不会再触发周期函数，说明此时vue实例已经解除了事件监听以及和dom的绑定，但是dom结构依然存在

[[↑] Back to top](#vue问题)

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

[[↑] Back to top](#vue问题)

### 说下你对mvvm的理解，双向绑定的理解

mvvm就是vm框架视图、m模型就是用来定义驱动的数据、v经过数据改变后的html、vm就是用来实现双向绑定
双向绑定:一个变了另外一个跟着变了，例如：视图一个绑定了模型的节点有变化，模型对应的值会跟着变

[[↑] Back to top](#vue问题)

### vue-router有哪几种导航钩子

三种，
第一种：是全局导航钩子：`router.beforeEach(to,from,next)`，作用：跳转前进行判断拦截。
第二种：组件内的钩子
第三种：单独路由独享组件

[[↑] Back to top](#vue问题)

### Vue如何实现双向绑定

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

[[↑] Back to top](#vue问题)
