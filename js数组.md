---
title: js数组
date: 2020-03-22 22:42:03
tags:
- web
- 数组
categories: 
- 学习笔记
- javaScript
---

## **ARRY数组** <sup>[link-MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)</sup>

### 1. **定义**
---

数组是按一定次序排列的一组值. hash结构, 存在位置对应的编号. 是数据的集合. 

此处的数据可以是其中基本数据类型, 当数组的元素还是数组时, 就构成多维数组. 
<br>

### 2. **本质**
---

本质上数组Array就是一个对象, 它的构造函数是Array. 读取时要注意的是数组只支持[]结构, 即arr[].
<br>

### 3. **属性**
---

1. **length 返回成员数量**
   1. 是一个动态的值
   2. 总是比最大的键名大1
   3. 人为可写, 当设置为0时则清空数组
2. **in 检查某个键名是否存在**
   1. 即适用于对象也适应于数组    2 in arr    //  true
3. **for...in... 遍历所有键**
   1. 推荐使用for循环获得纯净的数值键对应的数组
   2. ```js for (var key in a) {console.log(key);} ```
<br>

### 4. **伪数组**
---

包含有数组的特点的Object对象, 具有键值对和length属性, 但是原型链中没有push等只有数组具备的方法(Array.prototype)

即数组的arr.__proto__=Array.prototype

目前的伪数组有  
1. argument 对象
2. 大多数 DOM 元素集, 即*document.querySelectAll('div') 返回的对象*

通过slice方法可以将“类似数组的对象”变成真正的数组. 
```js
var arr = Array.prototype.slice.call(arrayLike);
```

```js
//  arguments 调用  forEach 方法 
function logArgs() {
  Array.prototype.forEach.call(arguments, function (elem, i) {
    console.log(i + '. ' + elem);
  });
}

// 等同于 for 循环
function logArgs() {
  for (var i = 0; i < arguments.length; i++) {
    console.log(i + '. ' + arguments[i]);
  }
}
```
<br>