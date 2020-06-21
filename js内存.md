---
title: js内存
date: 2020-02-25 09:59:25
tags:
- web
- 内存
categories: 
- 学习笔记
- javaScript
---

# 单线程的Javascript实现异步[简]

## 什么事单线程

单线程语言缺乏并发机制,也就是说,如果一个进程运行过久将会阻塞其他进程,这会导致超时timeout,浏览器会提醒kill the process

尽管js是单线程语言,但是借助浏览器的web API,队列回调(Call back queue)和时间循环机制(Event loop mechanism)可以实现异步

## Javascript environment

![img](https://i.loli.net/2020/02/25/F1vM2ty4K3an5Hj.png)

### heap 堆

Heap 用于存储对象Object,声明一个变量便会申请一块存储区域

### stack 栈

栈保存我们的函数调用。在每个新函数调用中，它都被推入堆栈的顶部。通过堆栈跟踪在JavaScript上出现异常时，可以看到栈

### Web API

浏览器内置了API，开发人员可以使用它们进行复杂的流程

### Callback queue

当进程完成其工作（例如xhr调用）时，它会被放入回调队列中。 栈为空后，事件循环进程将触发回调队列，这意味着该进程在该队列中等待，直到栈为空。 一旦我们的栈没有函数调用，就会从回调队列中弹出一个进程并将其推入栈。

### Event loop

一个检查栈里面的函数调用, 并连续出发CQ

---

### 例子

ctrl shift i  ||  F12 进入开发者模式
console中输入如下命令,观察输出

```javascript
console.log("hh");
setTimeout(() => {
console.log("you suck");
},1000);
console.log("dumb");

```

过程解析:

1. 首先,console调用,会被推stack进行函数调用
2. 然后变量'hh'被存入heap
3. 由于console不是异步调用,所以直接输出hh
4. 然后EL检查回收清空
5. setTimeout函数调用,推入stack
6. 这是一个异步函数,而且一个Web API函数。它将被推送到Web API框中，并且setTimeout函数将从stack中删除
7. console调用重复1-4
8. 当time计时结束,timeout函数进入回调队列中
9. 当stack为空的时候,El--->CQ
10. console.log(you suck)被推入stack重复与1-4

## TIPS

一. 浏览器划分给js引擎的有两块区域
- 代码区:存放代码
- 数据区: 存放数据
- eg: var a = 1,其中a在代码区,1再shujuqu

二. 对于简单的数据,如string number等直接存在stack中, 复杂数据(对象),在stack存放ADDR地址,在heap中存放数据

三.垃圾回收机制GC

- 一个对象没有被引用(stack没有对应ADDR)
- 它是垃圾
- 它将被回收

若不回收将导致内存泄漏 (IE那二货就这德性)
