---
title: 学习速记-html-ccs
date: 2020-02-11 15:16:44
categories: 
- 学习笔记
tags: 
- web
---



---

### HTML

---



- ##### input

  - ###### checkbox属性的input标签用label标签包裹

    ```html
    <label><input type="checkbox" value="hahaha" name="test"></label>
    ```




  - ###### radio属性input标签使用同一个name即标识为单选框

    ```html
    <input type="checkbox" name="van" value="cosplay">玩一下
    <input type="checkbox" name="van" value="trueplay">van一下
    ```

  

- ##### select<可选属性 multiple>

  ```html
  <select name="pets" id="pet-select">
      <option value="">--Please choose an option--</option>
      <option value="dog" disabled>Dog</option>   //不可选中
      <option value="cat" selected>Cat</option>	//默认选中
  </select>
  ```




- ##### table  <属性 collspace控制间隙>

- ##### span间由默认空格

  - ```html
    <span></span>
    <span></span>
    //改成即可
    <span></span><span></span>
    ```





---

### CSS

---

- ##### clearfix

  - ###### clearfix介绍：

  - 这是一个历史悠久的bug，当**两个浮动的元素**要实现**并排**时就会出现这样的bug，页面的其他元素会发生堆叠

  - ###### clearfix强制清除子级<a href="https://css-tricks.com/snippets/css/clear-fix/">On css tricks</a>

    - ```htmlh
      .group:after {
        content: "";
        display: table;
        clear: both;
      }					
      //这是clearfix的css修正代码
      ```

      ```HTML
      <div class="group">				//在父级使用clearrfix
        <div class="is-floated"></div>
        <div class="is-floated"></div>
        <div class="is-floated"></div>
      </div>
      //这是使用实际例子，在子元素上添加float，然后就可以让他们在同一行上排列
      ```

  - ###### [clearfix更多历史](https://css-tricks.com/clearfix-a-lesson-in-web-development-evolution/)

  

- ##### 类选择器写法

  - ```css
    .class .childrenclass1 .childrenclass2{
    	//注意类之间有空格
    }
    ```

  - ```css
    body nav div ul li a{
    	//标签名层级写法
    }
    ```

  - ```css
    .class nav div ul{
    	//混合写法
    }
    ```

  - ```css
    .class nav>div>ul{
    	//严格遵循>的层级寻找对应的标签添加css
    }
    ```

  

- ###### Chrome使用

  - style可查看元素的样式，上部分为自己编写的，下部分为浏览器默认样式

  - computed为计算出来的属性，实际浏览器效果

  - 取色时应该查看源代码，浏览器渲染那会改变颜色，取色器取色不是特别准确

    

- ###### 鼠标悬停操作hover解决添加border导致布局改变（开发者工具可以强制开启hover状态）

  - ```css
    .class{
    	border: 3px soild transparent;
    }
    .class:hover{
    	border: 3px soild red
    }
    //在原来的类上添加一个透明的border即可，其他会改便布局的属性同样可以使用这个思路
    ```




- ##### 取消默认格式以防影响padding&&margin

  - body，h1，h2......,ul,a,p等你不需要默认格式的paddding，margin等，可以

    ```css
    你不想要的默认属性标签｛ padding: 0px; margin: 0px｝
    ```




- ##### 块高度&&内联高度

  - ###### 块高度：div高度由块内部**文档流**元素高度决定

    - 文档流：文档内元素流动的方向，【块：自上而下，内联：自左而右】
    - 让块实现左到右流动，一：display：inline-block；（有bug）；二：clearfix实现
    - bug：内联元素在文档流排列，遇到阻断(如浏览器边界)，就会自动切割border，而不是形成两个border，完整的内容会被视为一个整体，不会被切割或显示(例如hhhhhhhh遇到浏览器边界，后面部分就会显示，而中文连在一起时也一样)；----->解决的办法就是添加wordbreak属性
    
  - ###### 内联高度：内联元素由建议行高以及其他因素影像（图形学≈玄学）
  
    - 字体相关：[行高line-height(默认1.4倍字体大小)](https://css-tricks.com/fun-line-height/)；[字体图形知识](https://css-tricks.com/what-is-vertical-align/)；
    - 不同字体会有不同的行高展示效果
    - 浏览器也会有影响
  
  
  
- ##### 脱离文档流


  - position：fixed；脱离父元素，**改变父级元素高度**，相对窗口定位，元素**自动内缩**，而非填充

  - 父元素position：relative；子元素position：absolute；子元素相对父元素定位；[定位相关](https://css-tricks.com/almanac/properties/t/top-right-bottom-left/)

    

- ##### height与width--两大css未解之谜


  - height和width为表示属性可以覆盖原来的元素长宽；

  - 内联元素默认不接受，但通过设置可以实现


    - ```css
      img {
        width: 400px !important;
      }
      ```

      

  - height：无法使用100%来表示值

  - width：100%=元素的大小*100+内外距离、行高、默认样式等


    - 解决：包裹div，添加clearfix即可

  - 尽量避免使用这两属性，容易出bug！！！！

  

- ##### css画图：[link](https://css-tricks.com/the-shapes-of-css/)

- ###### svg上下margin不一致：vertical-align：top重置即可