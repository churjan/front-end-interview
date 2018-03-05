# CSS问题

## 目录

* [如何垂直居中一个元素](#如何垂直居中一个元素)
* [字体font-family](#字体font-family)
* [什么是BFC 如何触发BFC](#什么是BFC-如何触发BFC)
* [请写出圣杯布局和双飞翼布局](#请写出圣杯布局和双飞翼布局)

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
https://juejin.im/entry/58296b1a570c3500587bb553

[[↑] Back to top](#css问题)

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

[[↑] Back to top](#css问题)

### 什么是BFC 如何触发BFC

BFC全称为block formatting context,中文为“块级格式化上下文”。具有 BFC特性的元素可以看作是隔离了的独立容器，容器里面的元素不会在布局上影响到外面的元素，并且BFC具有普通容器所没有的一些特性。

触发 BFC

1. `<HTML>`根元素
1. 浮动元素：float 除 none 以外的值
1. position 的值不为 relative 和 static
1. display 为 inline-block、table-cells、flex
1. overflow 除了 visible 以外的值 (hidden、auto、scroll)

[[↑] Back to top](#css问题)

### 请写出圣杯布局和双飞翼布局

参考：  
https://segmentfault.com/a/1190000013301463

[[↑] Back to top](#css问题)