### 如何使下面程序输出1，2，3

```js
for(var i = 0; i < 3; i++) {
    setTimeout(() => {
        console.log(i)
    })
}
// 3
// 3
// 3
```

<details>
<summary>参考答案</summary>

```js
// 方法一:
for(var i = 0; i < 3; i++) {
    (function(i) {
        setTimeout(() => {
            console.log(i)
        })
    })(i)
}

//方法二：
for(let i = 0; i < 3; i++) {
    setTimeout(() => {
        console.log(i)
    })
}

```

</details>

### 求契波那切数列第n个数的值

```text
契波那切数列  1、1、2、3、5、8......,从第三个数开始，每个数都是前两个数的和
```

<details>
  <summary>参考答案</summary>

  ```js
  const fibo=(n)=>n>2?fibo(n-1)+fibo(n-2):n;
  ```

</details>

### 首字母大写

```text
this is a pen => This Is A Pen
```

<details>
  <summary>参考答案</summary>

```js
function bigLetter(str){
  return str.toLowerCase().replace(/\b\w+\b/g, function(word){
    return word.substring(0,1).toUpperCase()+word.substring(1);
  });
}
```

</details>

### 统计字符串中字母个数

```text
例：统计字符串 aaaabbbccccddfgh 中字母个数
```

<details>
  <summary>参考答案</summary>

```js
let str='aaaabbbccccddfgh';
let obj={};
Array.from(str).forEach(char=>{
  if(!obj[char]){
    obj[char]={
      count:1,
      name:char
    }
  }else{
    obj[char].count++;
  }
})
let result=Object.values(obj).map(item=>`${item.name}=${item.count}`).join('\n');
console.log(result)
```

</details>

### 手写防抖，节流

<details>
  <summary>参考答案</summary>

```js
//防抖
function debounce(cb,delay=300){
  return function(...args){
    clearTimeout(timer.id);
    timer.id=setTimeout(()=>{
      cb.apply(this,args);
    },delay)
  }
}

//节流
function throttle(cb,interval=300){
  return function(...args){
    if(!timer.id){
      timer.id = setTimeout(() => {
          fn.apply(this, args);
          timer.id = null;
      }, interval)
    }
  }
}
```

</details>

### 写一个sum方法，可以实现以下两种调用方式

```js
console.log(sum(2,3)) //5
console.log(sum(2)(3)) //5
```

<details>
  <summary>参考答案</summary>

  ```js
    const sum=function(x,y){
      if(y===undefined){
        return function(y){
          return x+y;
        }
      }else{
        return x+y;
      }
    }
  ```

<details>

### 手写一个深拷贝

<details>
<summary>参考答案</summary>

```js
function cloneDeep (target) {
    function checkType(target) {
        return Object.prototype.toString.call(target).slice(8, -1)
    }
    var result, checkedType = checkType(target)
    if (checkedType === 'Array') {
        result = []
    } else if (checkedType === 'Object') {
        result = {}
    } else {
        return target
    }
    //递归遍历对象或数组中的属性值或元素为原始值为止
    for (var key in target) {
        if ( checkType(target[key]) === 'Array' || checkType(target[key]) === 'Object') {
            result[key] = cloneDeep(target[key])
        } else {
            result[key] = target[key]
        }
    }
    return result
}
```

</details>
