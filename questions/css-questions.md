# CSS问题

## 目录

* [css的权重优先级](#css的权重优先级)
* [如何垂直居中一个元素](#如何垂直居中一个元素)
* [什么是BFC?如何触发BFC](#什么是bfc如何触发bfc)
* [请写出三列自适应布局](#请写出三列自适应布局)

### css的权重优先级

`!important > 行内样式 > ID > 类、伪类、属性 > 标签名 > 继承 > 通配符`

[[↑] Back to top](#css问题)

### 如何垂直居中一个元素

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

参考：  
[https://juejin.im/entry/58296b1a570c3500587bb553](https://juejin.im/entry/58296b1a570c3500587bb553)

[[↑] Back to top](#css问题)

### 什么是BFC?如何触发BFC

BFC全称为block formatting context,中文为“块级格式化上下文”，它是指一个独立的块级渲染区域，只有Block-level Box参与，该区域拥有一套渲染规则来约束块级盒子的布局，且与区域外部无关。具有BFC特性的元素可以看作是隔离了的独立容器，容器里面的元素不会在布局上影响到外面的元素，并且BFC具有普通容器所没有的一些特性。

触发 BFC

1. `<HTML>`根元素
1. 浮动元素：float 除 none 以外的值
1. position 的值不为 relative 和 static
1. display 为 inline-block、table-cells、flex
1. overflow 除了 visible 以外的值 (hidden、auto、scroll)

[[↑] Back to top](#css问题)

### 请写出三列自适应布局

e.g. 左边宽200px，右边宽150，中间自适应

```html
//方法一：左右浮动+中间100%宽度
//圣杯布局
<style type="text/css">
.container {
  padding-left: 200px;
  padding-right: 150px;
  overflow: hidden;
}
.container div {
  height: 150px;
  line-height: 150px;
  float: left;
}
.center {
  width: 100%;
  background-color: #50bf3c;
}
.left {
  width: 200px;
  margin-left: -100%;
  position: relative;
  left: -200px;
  background-color: #ff5722;
}
.right {
  width: 150px;
  margin-left: -150px;
  position: relative;
  left: 150px;
  background-color: #2196f3;
}
</style>
<div class="container">
  <div class="center">中间自定义</div>
  <div class="left">左侧定宽</div>
  <div class="right">右侧定宽</div>
</div>

//双飞翼布局
<style type="text/css">
.container {
  overflow: hidden;
}
.container div {
  height: 150px;
  line-height: 150px;
}
.center-wrap{
  width:100%;
  float: left;
}
.center {
  margin-left:200px;
  margin-right:150px;
  background-color: #50bf3c;
}

.left {
  width: 200px;
  margin-left: -100%;
  background-color: #ff5722;
  float: left;
}
.right {
  width: 150px;
  margin-left: -150px;
  background-color: #2196f3;
  float: left;
}
</style>
<div class="container">
  <div class="center-wrap">
      <div class="center">中间自定义</div>
  </div>
  <div class="left">左侧定宽</div>
  <div class="right">右侧定宽</div>
</div>

//方法二：绝对定位+中间不给宽度
<style type="text/css">
.container {
  position: relative;
}
.container div {
  height: 150px;
  line-height: 150px;
}
.center {
  background-color: #50bf3c;
  margin-left: 200px;
  margin-right: 150px;
}
.left {
  width: 200px;
  background-color: #ff5722;
  position: absolute;
  top: 0px;
  left: 0px;
}
.right {
  width: 150px;
  background-color: #2196f3;
  position: absolute;
  top: 0px;
  right: 0px;
}
</style>
<div class="container">
  <div class="center">中间自适应</div>
  <div class="left">左侧定宽</div>
  <div class="right">右侧定宽</div>
</div>

方法三：flex
<style type="text/css">
.container{
  display:flex;
}
.left{
  flex-basis:200px;
}
.right{
  flex-basis:150px;
}
.center{
  flex-grow:1;
}
</style>
<div class="container">
  <div class="left">左侧定宽</div>
  <div class="center">中间自适应</div>
  <div class="right">右侧定宽</div>
</div>

```

[[↑] Back to top](#css问题)
