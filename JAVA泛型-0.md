---
title: JAVA泛型
date: 2020-04-18 18:04:37
tags:
---
![java泛型.png](https://i.loli.net/2020/04/18/cPSXt7feylCEALd.png)

# java泛型
<br><br><br>
## 一 通常情况下为了表示变量可以接受不同类型的数据(如: 坐标接受int, float, string等)

<br><br>

### 1.传统(IDK1.5以前):
利用**向上转型和自动装箱**可以实现将所有原始数据封装为object类型

向下转型存在风险, 编译时不易发现错误
重载有重复代码

- int --> Integer --> Object
- double -->Double --> Object
- String --> Object

<br><br>

### 2.泛型:
所谓“泛型”，就是“宽泛的数据类型”，任意的数据类型。

<hr>

- 泛型类

	- public fuck<T>{}

- 泛型方法

	- public  <T> void fuck ( T  x){}

		- 修饰符 <类型参数列表> 返回类型 方法名(形参列表) { 方法体 }

- 泛型接口

	- public interface fuck<T>{}

		- 实现:
public damn<T> implement fuck<T>{}

<hr>
<br><br><br>

## 二 传值参数（我们通常所说的参数）由小括号包围，如 (int x, double y)
<hr>
<br><br><br>

## 三 类型参数（泛型参数）由尖括号包围，多个参数由逗号分隔，如 <T> 或 <T, E>。

###  1.特点

- 不但数据的值可以通过参数传递，数据的类型也可以通过参数传递
- T1, T2 是自定义的标识符，也是参数，用来传递数据的类型，而不是数据的值，我们称之为类型参数
- 泛型类在实例化时必须指出具体的类型，也就是向类型参数传值，格式为：
className variable<dataType1, dataType2> = new className<dataType1, dataType2>();

### 2.限制泛型

- 用户传递其他数据类型可能会引起错误

	- 例如 某些类型不支持其他类型的方法,doubleValue不支持IString的对象调用

- 通过 extends 关键字
- <T extends Number> 表示 T 只接受 Number 及其子类，传入其他类型的数据会报错。
extends理解为 T 是继承自 Number 类的类型，或者 T 是实现了 XX 接口的类型

<hr>
<br><br><br>

## tip: 方法声明

### 访问权限>>方法类型>>返回类型>>方法名称>>参数列表>>方法体

- 方法声明

	- ①修饰符：修饰符，这是可选的，告诉编译器如何调用该方法。定义了该方法的访问类型。
	- ②返回值类型 ：方法可能会返回值。returnValueType 是方法返回值的数据类型。有些方法执行所需的操作，但没有返回值。在这种情况下，returnValueType 是关键字void。
	- ③方法名：是方法的实际名称。方法名和参数表共同构成方法签名。
	- ④参数类型：参数像是一个占位符。当方法被调用时，传递值给参数。这个值被称为实参或变量。参数列表是指方法的参数类型、顺序和参数的个数。参数是可选的，方法可以不包含任何参数。
	- ⑤方法体：方法体包含具体的语句，定义该方法的功能。

<hr>
<br><br><br>