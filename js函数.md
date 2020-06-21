---
title: js函数
date: 2020-03-09 22:36:43
tags:
- web
- 函数
categories: 
- 学习笔记
- javaScript
---

![函数.png](https://i.loli.net/2020/03/09/DAzCsfO4rwlqa5Z.png)


# 函数

## 函数的5中声明方式
### 关键字
- function x('参数1','参数2'){
	return undefined
}
### 匿名函数
- var foo = function ('参数1','参数2'){return}
### 具名函数 = function
- var foo = function fun( '参数',''){return}//*console.log(fun)会打印出fun未定义;但是关键字声明的话可以直接访问*
### new
- new Function('x','y','return x+y')
### =>箭头函数(匿名)
- f = (x,y) => {return x+y}
### 匿名函数的.name方法
- var f2 = function() {}	//f2.name= f2
- var f3 = function f4(){}	//f3.name = f4
## 如何调用函数
### 概述
- 函数就是可以反复调用的代码块,接受不同的参数,返回不同的值
### 函数的存储
- 可以执行代码块的对象,存储形式与Object一致
### function.prototype
- call
- apply
- bind 
### 调用形式 
- f(x,y)	//简写
- f.call(undefined,x,y)	//真正用法
## 什么是Call Stack(先进后出)(调用栈)
- 每进入一个函数的时候先标记位置,然后return的时候带回返回值,并回到上一个节点 (递归原理)
- stack overfollow(栈溢出): 最多压进栈内的长度为10000左右
## this和arguments关键字(历史原因引入this)
### 来源于call
- f.call(undeifined,x,y)
	- call的第一个参数就是this,可以用this得到
	- call的参数可以用arguments得到
	- arguments产生一个伪数组
### 规则
- 普通模式下this为undefined时,会被替换为window
- 'use strict'模式下则输出undefined
## 作用域(scope)(树结构)
### 原则
- 只要有函数就有一个作用域
- 就近原则
- 变量提升(注意声明 )
### 全局作用域
- 子作用域1
- 子作用域2
	- 子作用域2.2
- 子作用域3
### a=3
- 当全局没有var a声明时,a = 1将被认为时声明并赋值
- 当全局有var 声明时,a = 1优先被认为是赋值

## 闭包
- 如果一个函数使用了它范围外的值,那么	这个函数+这个变量 就是闭包
