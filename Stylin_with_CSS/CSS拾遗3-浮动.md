[TOC]
# 浮动
CSS 设计float 属性的主要目的，是为了实现文本绕排图片的效果。然而，这个属性居然也成了创建多栏布局最简单的方式。
## 1. 文本绕排图片
<<<<<<< HEAD
```css
=======
```
>>>>>>> refs/remotes/origin/master
<img …… />
<p>…the paragraph text…</p>
CSS 规则如下。
/*为简明起见，省略了字体声明*/
p {margin:0; border:1px solid red;}
/*外边距防止图片紧挨文本*/
img {float:left; margin:0 4px 4px 0;}
```
![](leanote://file/getImage?fileId=59f68725ab64410d21000ab2)
>浮动非图片元素时，必须给它设定宽度，否则后果难以预料。图片无所谓，因为它本身有默认的宽度。

## 2. 创建分栏
<<<<<<< HEAD
```css
=======
```
>>>>>>> refs/remotes/origin/master
p {
    float: left;
    margin: 0;
    width: 200px;
    border: 1px solid red;
}

img {
    float: left;
    margin: 0 4px 4px 0;
}
```
![](leanote://file/getImage?fileId=59f68bceab64410d21000bdc)

## 围住浮动元素的三种方法

- 为父元素添加overflow:hidden
- 同时浮动父元素
- 在父元素内容的末尾添加非浮动元素，可以直接在标记中加，也可以通过给父元素添加clearfix 类来加

>没有父元素时最简单的办法就是给一个浮动元素应用clear:both，强迫它定位在前一个浮动元素下方