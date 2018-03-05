# HTML问题

## 目录

* [重排和重绘](#重排和重绘)
* [什么情况会触发回流和重绘](#什么情况会触发回流和重绘)
* [详说Cookie, LocalStorage与SessionStorage](#详说cookie-localstorage与sessionstorage)

### 重排和重绘

1. 部分渲染树（或者整个渲染树）需要重新分析并且节点尺寸需要重新计算。这被称为重排。注意这里至少会有一次重排-初始化页面布局。
1. 由于节点的几何属性发生改变或者由于样式发生改变，例如改变元素背景色时，屏幕上的部分内容需要更新。这样的更新被称为重绘。

[[↑] Back to top](#html问题)

### 什么情况会触发回流和重绘

会导致回流的操作：

1. 页面首次渲染
1. 浏览器窗口大小发生改变
1. 元素尺寸或位置发生改变
1. 元素内容变化（文字数量或图片大小等等）
1. 元素字体大小变化
1. 添加或者删除可见的DOM元素
1. 激活CSS伪类（例如：:hover）
1. 查询某些属性或调用某些方法

会导致回流的操作：

当页面中元素样式的改变并不影响它在文档流中的位置时（例如：color、background-color、visibility等）。

参考：  
[https://juejin.im/post/5a9923e9518825558251c96a?utm_source=gold_browser_extension](https://juejin.im/post/5a9923e9518825558251c96a?utm_source=gold_browser_extension)

[[↑] Back to top](#html问题)

### 详说Cookie, LocalStorage与SessionStorage

|特性|Cookie|localStorage|sessionStorage|
|----|----|----|----|
数据的生命期|可设置失效时间，默认是关闭浏览器后失效|除非被清除，否则永久保存|仅在当前会话下有效，关闭页面或浏览器后被清除
存放数据大小|4K左右|一般为5MB|一般为5MB
与服务器端通信|每次都会携带在HTTP头中，如果使用cookie保存过多数据会带来性能问题|仅在客户端（即浏览器）中保存，不参与和服务器的通信|仅在客户端（即浏览器）中保存，不参与和服务器的通信
易用性|需要程序员自己封装，源生的Cookie接口不友好|源生接口可以接受，亦可再次封装来对Object和Array有更好的支持|源生接口可以接受，亦可再次封装来对Object和Array有更好的支持

参考:  
[https://segmentfault.com/a/1190000002723469](https://segmentfault.com/a/1190000002723469)

[[↑] Back to top](#html问题)
