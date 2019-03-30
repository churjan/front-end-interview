### 求契波那切数列第n个数的值

```js
//契波那切数列  1、1、2、3、5、8......,从第三个数开始，每个数都是前两个数的和
const fibo=(n)=>n>2?fibo(n-1)+fibo(n-2):n;
// fibo(1) ==> 1
// fibo(2) ==> fibo(1)+fibo(0) ==> 1+0;
// fibo(3) ==> fibo(2)+fibo(1) ==> fibo(1)+fibo(0)+1 ==> 1+0+1
```
### 找出一个数组中重复的元素

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

### 首字母大写

`this is a pen => This Is A Pen`

```js
function bigLetter(str){
  return str.toLowerCase().replace(/\b\w+\b/g, function(word){
    return word.substring(0,1).toUpperCase()+word.substring(1);
  });
}

```

### 统计字符串中字母个数或统计最多字母

```js
let str='aaaabbbccccddfgh';
let obj={};
Array.from(str).forEach(char=>{
  if(!obj[char]){
    obj[char]={
      count:1,
      val:char
    }
  }else{
    obj[char].count++;
  }
})
let result=Object.values(obj).map(item=>`${item.val}=${item.count}`).join(' ');
console.log(result)
```
