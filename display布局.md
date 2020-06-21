---
title: display布局
date: 2020-02-19 22:18:47
tags:
- css
- display
categories: 学习笔记
---

## 一 关于display

所有元素在网页上的存在形式都是长方体,而影响网页的布局的主要因素一方面是[文档流](https://www.bukun.top/2020/02/11/%E5%AD%A6%E4%B9%A0%E9%80%9F%E8%AE%B0-html-ccs/#%E5%9D%97%E9%AB%98%E5%BA%A6-amp-amp-%E5%86%85%E8%81%94%E9%AB%98%E5%BA%A6),一方面则是css控制的元素的表现形式display,其中常用的有:

```css
div {
  display: inline;        /* Default of all elements, unless UA stylesheet overrides */
  display: inline-block;  /* Characteristics of block, but sits on a line */
  display: block;         /* UA stylesheet makes things like <div> and <section> block */
  display: run-in;        /* Not particularly well supported or common */
  display: none;          /* Hide */
}
```

所有元素默认的样式都是**inline**内联,而浏览器的用户代理脚本([UA stylesheet](https://stackoverflow.com/questions/12582624/what-is-user-agent-stylesheet))会改变大部分的元素为**block**块

## 二 概略<sup>[**MDN**](https://developer.mozilla.org/en/CSS/display)<sup/>

### inline 内联

- 元素的默认值,eg:  span em b.....

- 不会破坏文本的流动,以基线为准和其他元素保持在同一行内![this](https://i0.wp.com/css-tricks.com/wp-content/uploads/2011/09/inline-element.png?w=346&ssl=1)

- 使用margin和padding会在水平方向扩张但不会再垂直方向扩张,但不接受width height的值
![css-tricks](https://i1.wp.com/css-tricks.com/wp-content/uploads/2011/09/inlinepadding.png?w=519&ssl=1)

### inline-block 内联块

- 基本与内联一致,但是不同的是有以下两点
  - 接受width height
  - 水平和垂直方向的边距都会扩张
  ![css-tricks](https://i0.wp.com/css-tricks.com/wp-content/uploads/2011/09/inline-block.png?w=526&ssl=1)
  
### block 块

- div\section\ul\p\h#....等会被浏览器设置为block显示
- 块级元素不会[内联](https://developer.mozilla.org/en-US/docs/Web/HTML/Inline_elements),但是会跨过内联元素而被分割
![css-tricks](https://i2.wp.com/css-tricks.com/wp-content/uploads/2011/09/block.png?w=520&ssl=1)

### run-in 嵌入

- 火狐不支持
- 嵌入元素(如报纸首行前面的大字)
  ![css](https://i1.wp.com/css-tricks.com/wp-content/uploads/2011/09/Run-in.png?resize=294%2C97)

### **flex 弹性**

- ####  背景
  
  Flexbox Layout（弹性盒）（W3C 2017推荐模块）的目标是提供一种更有效的方式来布置，元素在一个容器中对齐和分配空间，即使大小未知或者是动态的（单词“ flex”的来由）。

  flex布局的主要思想是**使容器能够更改其项目的宽度/高度（和顺序）**，以**最好地填充**可用空间（用于适应显示设备和屏幕尺寸）。Flex容器会将元素扩大以填充可用的可用空间，或收缩它们防止溢出。

  与常规布局（**基于垂直的块和基于水平的内联块**）相比，**flexbox布局与方向无关**。尽管这些样式对于页面效果很好，但是它们缺乏灵活性来支持大型或复杂的应用程序（尤其是在方向更改，调整大小，拉伸，缩小等方面）。

  *Flexbox适合app和小规模布局，而[Grid](#gird-%e7%bd%91%e6%a0%bc)布局则用于较大规模的布局*

- #### 图形知识
  ![basic](https://css-tricks.com/wp-content/uploads/2018/11/00-basic-terminology.svg)
  main axis:  主轴  
  cross axis: 交叉[横]轴  

- ####  基础与术语
  
- ##### 容器的属性
  
    1. display: flex //或者inline-flex,colum属性无效
    2. flex-direction: row | row-reverse | column | column-reverse;
       - row（默认值）：从左到右ltr；从右到左rtl
       - row-reverse：从右到左的ltr; 从左到右rtl
       - column：与row上至下相同
       - column-reverse：与row-reverse下至上相同
       - ![img](https://css-tricks.com/wp-content/uploads/2018/10/flex-direction.svg)
    3. flex-wrap: nowrap | wrap | wrap-reverse;   
      以不同的缠绕方式排列,分别为**一行||缠绕||反向缠绕**
       ![批注 2020-02-20 114204.png](https://i.loli.net/2020/02/20/sPGW1ERuAlMeDfT.png)

    4. flex-flow: <‘flex-direction’> || <‘flex-wrap’>缩写
    5. justify-content  
      分配顺着父容器主轴的弹性元素之间及其周围的空间
      ![img](https://css-tricks.com/wp-content/uploads/2018/10/justify-content.svg)
    6. align-items  
      justify在垂直方向的布局
      ![csst](https://css-tricks.com/wp-content/uploads/2018/10/align-items.svg)
    7. align-content  
      类似于将整体视为单个元素进行justify的排列
      ![csst](https://css-tricks.com/wp-content/uploads/2018/10/align-content.svg)

- ##### children元素的属性

    1. order  
      默认为零,按源代码的顺序排列元素,强制添加数字则可以排序
      ![csst](https://css-tricks.com/wp-content/uploads/2018/10/order.svg)
    2. flex-grow  
      设置分配比例,默认为1,平均分配||更换为2则改元素是其他元素的两倍(负值不可用)
      ![csst](https://css-tricks.com/wp-content/uploads/2018/10/flex-grow.svg)
    3. flex-shrink
      设置缩小比例,与grow类似
    4. flex-basis
      设置默认的获得扩充空间的比例,元素本身+其他空间,这里的其他空间会被分配给元素,和grow相关,添加grow的比例就会分配空间
      ![w3c](https://www.w3.org/TR/css-flexbox-1/images/rel-vs-abs-flex.svg)
    5. flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]   简写
    6. align-self
      对单个元素的对齐方式进行规定,用于覆盖align-items
      不支持float,clear,vertical-align


- [完全使用手册和案例--来自css-tricks](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
  
- [新旧flex一些差异[旧]](https://css-tricks.com/using-flexbox/)

### Gird 网格

- [待整理](https://css-tricks.com/snippets/css/complete-guide-grid/)
  
### none 隐藏

- 值得注意的是,隐藏后的元素还是存在与DOM中

### table-values 表格

- 与标签table的功能类似,但是不同的是有更多的语义表达

```css
div {
  display: table;/*<table>*/
  display: table-cell;/*<td>*/
  display: table-column;/* <col> */
  display: table-colgroup;/* <colgroup> */
  display: table-header-group;/*<thead>*/
  display: table-row-group;/*<tbody>*/
  display: table-footer-group;/*<tfoot>*/
  display: table-row;/*<tr>*/
  display: table-caption;/*<caption>*/
}
```

- 使用方式模仿表格

```css
<div style="display: table;">
  <div style="display: table-row;">
    <div style="display: table-cell;">
     It's suck!wubu labu dabuda!
    </div>
  </div>
</div>
```
