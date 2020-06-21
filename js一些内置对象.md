---
title: js一些内置对象
date: 2020-03-6 17:24:25
tags:
- web
- 对象
categories: 
- 学习笔记
- javaScript
---
<center>

>## 浏览器造的全局变量——window

*引言:  ECMSCRIPT 规定全局变量global,实际上就是浏览器事先声明的window对象,本质上window就是一个hash数组,存有不同的键值对,这些键值对就是一些常用的属性.*
<br><br><br>

### 概览

<center>

ECMA|浏览器
-------|-------
global.parseInt<br>global.parseFloat<br>global.Number<br>global.String<br>global.Boolean<br>global.Object<br>|window.alert<br>window.prompt<br>window.comfirm<br>window.console.log<br>window.console.dir<br>window.document<br>window.document.createElement<br>window.document.getElementById

[more on MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects)

</center>
<br><br><br><br><br><br>

### 全局函数

---
<br><br><br>

#### Number()

```js
 var a = 1
var int = new Number(1)
console.log(a === int)       //false
```
其中,new关键字实际上就是js诞生之初参照Java的产物;<br>而实际生产使用的var 关键字可以代替,因为其中有<br>

```js
a.toString()
//生命一个临时的变量temp存储a的值进行new(1),toString的操作,返回值之后再删除
```

#### String()

一些常见属性

```js
str.toString(16)//以16进制表示  
str.trim()//修剪多余的空格
str.concat(str2)//连接str,str2
str.slice(0,5)//切片str[0]-str[4]
str.replace('s1','s2')//替换
str.charcode()//获得ASCII编码
```

#### Boolean()
...
#### Object()
对象的值不相等,除非ADDR一致
<br><br><br><br><br><br>

### 公共属性

---
<br><br><br>

*如果每创建一个对象就封装一些相同的方法,如toString,将会造成大量的内存浪费;<br>所以有公共属性,其他对象调用时直接存储调用地址*

表示: __proto__(隐藏值)

调用过程↓
![未命名文件.png](https://i.loli.net/2020/03/06/OpW8YZSRLkgdGnN.png)

按照这个过程,有以下的等式成立<br>
**Object.proto === function.prototype**

```js

String.prototype === str.__proto__
//实际指向一致

//特别的,公共函数Object()的构造函数是function
//function既是Object,也是Function
Function.__proto__ === Object.prototype
Function.__proto__ === Function.prototype
Object.__proto__ === Function.prototype

```

</center>