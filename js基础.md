---
title: js基础
date: 2020-02-25 09:59:25
tags:
- web
- js
categories: 
- 学习笔记
- javaScript
---
## 一 概论

### 历史        [more](https://wangdoc.com/javascript/basic/history.html)

- Tim Berners-Lee--互联网之父:  
  1990年底,欧洲核能研究组织（CERN）科学家 Tim Berners-Lee，在全世界最大的电脑网络——互联网的基础上，发明了万维网（World Wide Web），从此可以在网上浏览网页文件。最早的网页只能在操作系统的终端里浏览，也就是说只能使用命令行操作，网页都是在字符窗口中显示，这当然非常不方便。
- Netscape网景:  
  92年,美国NCSA开发出第一个浏览器Mosaic;
  其中的一位主要的程序员Marc联合投资家Jim成立Mosaic通信,后改名网景,发布新一代浏览器,Netscape Navigation  
  为了实现浏览器行为的控制,需要一种页面嵌入的脚本.起初和Sun公司合作,嵌入java小程序(java applet),由于语法过重,最后决定自主开发
  
- Branden Eich:  
  由于公司的需要,新的脚本语言需要和java达到预期强大的推广性和易用性,branden在10天内编写完雏形Mocha,后改名livescript,再后版本改名为javascript

- ECM欧洲计算机制造商协会
  同期有微软的JScript同台竞争浏览器市场,最后netscape扛不住微软的封锁性质的专属物件,最后在倒闭前,开源netscape,后续由mozilla管理基金会,项目为firefox火狐  
  并向ECM申请规范,如今发布到ECM2019,但目前广泛学习使用为ECM'5和ECM'6标准
  
### 大杂烩JS

- 语法来源:  
  
  基本语法：借鉴 C 语言和 Java 语言.  
  数据结构：借鉴 Java 语言，包括将值分成原值和对象两大类.  
  函数的用法：借鉴 Scheme 语言和 Awk 语言，将函数当作第一等公民，并引入闭包  
  原型继承模型：借鉴 Self 语言（Smalltalk 的一种变种）  
  正则表达式：借鉴 Perl 语言。  
  字符串和数组处理：借鉴 Python 语言。 

- 核心语法

  1.基本语法结构: 操作符||控制结构||语句  
  2.标准库: 内置函数||对象  
  3.API:  
  浏览器控制类：操作浏览器  
  DOM 类：操作网页的各种元素  
  Web 类：实现互联网的各种功能  
  操作系统API: Node
  
- 由于雏形简单,且有多种语言的相似之处,并且初期缺乏各种功能,使其解决问题的思路变得五花八门,致使javascript的编程风格一直都是面向对象和函数式编程

### 发展

- 浏览器平台化使Javascript向通用系统语言发展
- Node服务器端使前后端通用javascript可实现
- 移动平台应用开发Vue,react,angular
- 跨平台应用
- Jeff Atwood :Atwood定律--所有可以用js编写的程序,最后都会用js编写

## 数据类型

### 基本数据类型(ECM5)

|  Type   | example  | typeof |  falsy |
|  ----  | ----  |  ----  | ---- |
| Number  | int  float | number | 0,NaN |
| String  | '' 'hello' ' ' |  string  | '' |
| Boolean  |  true  false| boolean | |
| Undefined  | undefined | undefined| undefined |
| Null  | null |  object(bug)  | null|
| Object  | foo,{},[] | function(bug  )||

### 转化

|number| string | boolean |
| - | -| -|
| Number('1')<br>parseInt('1',10)<br>parseFloat('1.01')<br>'1' - 0 <br> +'1' |  toString()<br>null&&undefined ×<br>valueof.toString()<br>{Object:Object} | Boolean()<br>见上表falsy值 |

### TIPs

- javascript以64位双精度浮点数存储数字
- 以16位存储字符
- 1+'1' = 11 +会让其中不是字符串的转化为字符串再相加
- null和undefined极其相似  
  由于历史原因,js设计之初采用了C语言null可以转换为0的传统,像java一样被当作是一个对象.但是Branden认为表示'无'的最好不是对象,这样不容易发现错误. 故设计:null是一个表示“空”的对象，转为数值时为0；undefined是一个表示"此处无定义"的原始值，转为数值时为NaN.[more](https://wangdoc.com/javascript/types/null-undefined-boolean.html)
- 数值的标识  
  |10 | 8| 16|  2 |
  |-|-|-|-|
  | × | 0o | 0x | 0b|

  