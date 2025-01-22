---
title: js常用数组字符串方法
date: 2022-06-29 13:44:15
categories:
- 技术
tags:
- 前端
- js
---
## 数组常用方法
### <font color=#f5871f>1.push()</font>
数组尾部添加
```js
const arr = [1,2,3];
arr.push(4);
console.log(arr); //[1,2,3,4]
```
### <font color=#f5871f>2.pop()</font>
数组尾部弹出
```js
const arr = [1,2,3];
arr.pop();
console.log(arr); //[1,2]
```
### <font color=#f5871f>3.unshift()</font>
头部插入
```js
const arr = [1,2,3];
arr.unshift(0);
console.log(arr); //[0,1,2,3]
```
### <font color=#f5871f>4.shift()</font>
头部弹出
```js
const arr = [1,2,3];
arr.shift();
console.log(arr); //[2,3]
```
### <font color=#f5871f>5.concat()</font>
数组拼接
```js
const a=[1,2,3];
const b=[4,5]
a.concat(b); //[1,2,3,4,5]
```
### <font color=#f5871f>6.indexOf()和lastIndexOf()</font>
indexOf()：在数组中从前往后查找某个值，找到返回第一个符合值的下标，找不到返回-1
lastIndexOf()：在数组中从后往前查找某个值，找到返回第一个符合值的下标，找不到返回-1
```js
const arr = [1,2,3,4,5];
console.log(arr.indexOf(2)) //1 
console.log(arr.lastIndexOf(2)) //1 
```
### <font color=#f5871f>7.includes()</font>
查找值，找到返回true，找不到返回false
```js
const arr = [1,2,3,4,5];
console.log(arr.includes(2);) //true
```
### <font color=#f5871f>8.join()</font>
数组转换为字符串，括号里填连接方式，默认以逗号拼接
```js
const arr = [1,2,3,4,5];
console.log(arr.join()); //1,2,3,4,5
console.log(arr.join('.')); //1.2.3.4.5
```
### <font color=#f5871f>9.reverse()</font>
数组反向
```js
const arr = [1,2,3,4,5];
console.log(arr.reverse()) //[5,4,3,2,1]
```
### <font color=#f5871f>10.slice()</font>
slice(start,end):截取数组,从start到end,不包括end
```js
const arr = [1,2,3,4,5];
console.log(arr.slice(1,3)) //[2,3]
```
### <font color=#f5871f>11.splice()</font>
数组删除插入
splice(start,count,item1,item2,...)
从开始位置start开始删除count位的元素，添加item1,item2,...
count为0时为插入值
```js
const arr = [1,2,3,4,5];
const arr1 = arr.splice(1,2,'a','b');
console.log(arr); //[1,a,b,4,5]
console.log(arr1); //[2,3]
```

### <font color=#f5871f>12.sort()</font>
数组排序
```js
const arr = [1,2,3];
arr.sort((a,b)=>b-a)
console.log(arr);//[3,2,1]
```
### <font color=#f5871f>11.toString()</font>
数组转换为字符串
```js
const arr = [1,2,3];
console.log(arr.toString());//'1,2,3'
```

## 字符串常用方法
### <font color=#f5871f>1.charAt()</font>
返回指定位置的字符
```js
const str = '12345';
console.log(str.charAt(0));//1
```
### <font color=#f5871f>2.concat()</font>
字符串合并
```js
const a = '123';
const b = '345';
const c = a.concat(b);
console.log(c); //'123345'
```
### <font color=#f5871f>3.indexOf(),lastIndexOf()</font>
indexOf返回字符在字符串中首次出现的位置
lastIndexOf返回字符在字符串中最后一次出现的位置
```js
const str = 'abcdfa';
console.log(str.indexOf(a))//0
console.log(str.lastIndexOf(A))//5
```
### <font color=#f5871f>4.slice()</font>
```js
截取片段
const str = 'abcd';
console.log(str.slice(1,3))//bc
```
### <font color=#f5871f>5.split()</font>
使用分隔符分割字符串返回数组
```js
const str ='123';
console.log(str.split(''));// ['1','2','3']
```
### <font color=#f5871f>6.subtr(),substring()</font>
截取字符串片段
substr(start,length) 截取指定宽度的字符
substring(start,stop) 截取起点到终点的字符，不包含终点
```js
const str ='abcde';
str.substr(1,2);//bc
str.substring(1,3);//bc
```
### <font color=#f5871f>7.match()</font>
在字符串内检索指定的值或正则的匹配，返回一个数组。没找到返回null
```js
const str='abcdefedcba';
str.match('a');//['a', index: 0, input: 'abcdefedcba', groups: undefined]
str.match(/[a-z]/ig);//['a', 'b', 'c', 'd', 'e', 'f', 'e', 'd', 'c', 'b', 'a']
```
**注意事项：**正则表达式不加g，返回第一个符合的值的数组，包含input和index属性，index 属性声明的是匹配文本的起始字符在 str 中的位置，input 属性包含整个被搜索的字符串；正则加g，返回满足结果的数组集
### <font color=#f5871f>8.replace()</font>
replace接受2个参数，第一个是要替换掉的字符或正则的匹配，第二个参数是替换的字符或者回调函数
```js
const str = "Hello,World123";
str.replace('World','Jack'); //'Hello,Jack123'
const str = "Hello,World123";
str.replace(/\d/ig,function(i){
  console.log(i); //1 2 3
    return Number(i)+1;
}) //Hello,World234
```
### <font color=#f5871f>9.search()</font>
搜索正则匹配的字符，搜索到返回所在位置，没搜索到返回-1
```js
const str = "Hello,World123";
str.search(/H/ig);//0
```
### <font color=#f5871f>10.toLowerCase(),toUpperCase()</font>
toLowerCase()把字母转换成小写
toUpperCase()把字母转换成大写
```js
const str1 ='abcd';
const str2 = 'ABCD';
console.log(str2.toLowerCase()) //abcd
console.log(str1.toUpperCase()) //ABCD
```
### <font color=#f5871f>11.includes()</font>
检测字符串对象中是否包含某个字符，返回布尔值
```js
const str = 'Hello,world';
str.includes('Hello') //true
```
### <font color=#f5871f>12.repeat()</font>
返回一个新字符串，重复了指定次数的原字符串
```js
const str = 'a'
const str2 = str.repeat(3)
console.log(str2) //'aaa'
```