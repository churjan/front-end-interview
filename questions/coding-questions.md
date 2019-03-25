# Coding试题

## 求契波那切数列第n个数的值

```js
//契波那切数列  1、1、2、3、5、8......,从第三个数开始，每个数都是前两个数的和
const fibo=(n)=>n>=2?fibo(n-1)+fibo(n-2):n;
// fibo(1) ==> 1
// fibo(2) ==> fibo(1)+fibo(0) ==> 1+0;
// fibo(3) ==> fibo(2)+fibo(1) ==> fibo(1)+fibo(0)+1 ==> 1+0+1
```

## 找出一个数组中重复的元素

```js
//举例
arr = [1,2,3,4,1,1,2,4,4]
//输出 [1,2,4]
```

```js
Array.prototype.unique=function(){
  let array=this;
  let filter_array=[];
  array.forEach(item=>{
    if(!filter_array.includes(item)){
      filter_array.push(item)
    }
  })
  return filter_array;
}
```

## 首字母大写

`this is a pen => This Is A Pen`

```js
function bigLetter(str){
  bigStr = str.toLowerCase().replace(/\b\w+\b/g, function(word){
  return word.substring(0,1).toUpperCase()+word.substring(1);
  });
  return bigStr; 
}

```

## 统计字符串中字母个数或统计最多字母

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

## 请问上述代码在浏览器环境下，输出结果是多少

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
```

参考答案：

* [一道颇有难度的JavaScript题](https://cnodejs.org/topic/5867d50d5eac96bb04d3e302)

## 深拷贝

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

## 封装一个函数,参数是定时器的时间,`.then`执行回调函数

```js
function sleep (time) {

  return new Promise((resolve) => setTimeout(resolve, time));

}
```

## 请输出一下代码的输出结果

```js
setTimeout(function(){
    console.log(1)
},0);
new Promise(function(resolve){
    console.log(2)
    for( var i=100000 ; i>0 ; i-- ){
        i==1 && resolve()
    }
    console.log(3)
}).then(function(){
    console.log(4)
});
console.log(5);
```

参考：

* [https://juejin.im/entry/5aa0de54518825556b6c574b?utm_source=gold_browser_extension](https://juejin.im/entry/5aa0de54518825556b6c574b?utm_source=gold_browser_extension)
