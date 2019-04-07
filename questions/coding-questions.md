### 求契波那切数列第n个数的值

`契波那切数列  1、1、2、3、5、8......,从第三个数开始，每个数都是前两个数的和`

<details>
  <summary>参考答案</summary>

  ```js
  const fibo=(n)=>n>2?fibo(n-1)+fibo(n-2):n;
  ```

</details>

### 首字母大写

`this is a pen => This Is A Pen`

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
