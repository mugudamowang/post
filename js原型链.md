---
title: js原型链
date: 2020-03-23 11:42:03
tags:
- web
- 原型链
categories: 
- 学习笔记
- javaScript
---

## **原型链** <sup>[link-MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)</sup>
<br>

---
### 1. **概念**

每个实例对象（ object ）都有一个私有属性（称之为 __proto__ ）指向它的构造函数的原型对象（prototype ）该原型对象也有一个自己的原型对象( __proto__ ) ，层层向上直到一个对象的原型对象为 null.

*原型链*:    原型对象有着各种共用属性, 在访问属性过程中, 通过该对象和原型对象的层层搜索,直到尾端null的过程.
<br>

---
### 2. **继承**

js的继承基于原型链, 对象本质上是一个动态的属性包, 继承属性与其他属性,没有区别.

**调用this时,this指向当前继承的对象.而非原型对象**

```js
var o = {
  a: 2,
  m: function(){
    return this.a + 1;
  }
};

console.log(o.m()); // 3
// 当调用 o.m 时，'this' 指向了 o.

var p = Object.create(o);
// p是一个继承自 o 的对象

p.a = 4; // 创建 p 的自身属性 'a'
console.log(p.m()); // 5
// 调用 p.m 时，'this' 指向了 p
// 又因为 p 继承了 o 的 m 函数
// 所以，此时的 'this.a' 即 p.a，就是 p 的自身属性 'a' 
// from MDN
```
<br>

---
### 3. **prototype和__proto__**


**prototype是函数的属性**
这个属性是一个指针，指向一个对象，这个对象的用途就是**包含所有实例共享的属性和方法**（我们把这个对象叫做原型对象）。原型对象也有一个属性，叫做**constructor**，这个属性包含了一个指针，指回原构造函数

**__proto__是对象的属性**
对象具有属性__proto__，可称为隐式原型，一个对象的隐式原型指向构造该对象的构造函数的原型，这也保证了实例能够访问在构造函数原型中定义的属性和方法。

<small>[detail 1](https://www.zhihu.com/question/34183746)</small>

<small>[detail 2](https://www.zhihu.com/question/56770432/answer/315342130)</small>

![zhihu](https://pic1.zhimg.com/80/e83bca5f1d1e6bf359d1f75727968c11_720w.jpg)
<br>

---
### 4. **使用**

假设创建一个新的对象 function doSomething() {}

1. **添加属性**
    ```js
    function doSomething(){}
    doSomething.prototype.foo = "bar";
    console.log( doSomething.prototype );
    ```
2. **添加继承**
    ```js
    function doSomething(){}
    doSomething.prototype.foo = "bar"; // add a property onto the prototype
    var doSomeInstancing = new doSomething();
    doSomeInstancing.prop = "some value"; // add a property onto the object
    console.log( doSomeInstancing );
    ```
3. **打印出原型链**
    ```js
    {
    prop: "some value",
    __proto__: {
        foo: "bar",
        constructor: ƒ doSomething(),
        __proto__: {
            constructor: ƒ Object(),
            hasOwnProperty: ƒ hasOwnProperty(),
            isPrototypeOf: ƒ isPrototypeOf(),
            propertyIsEnumerable: ƒ
            propertyIsEnumerable(),
            toLocaleString: ƒ toLocaleString(),
            toString: ƒ toString(),
            valueOf: ƒ valueOf()
          }
      }
    }
    ```

即

 **doSomeInstancing.__ proto __ = doSomething.prototype**

**doSomeInstancing--->doSoemthing.prototype--->Object.prototype**