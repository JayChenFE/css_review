<!-- TOC -->

- [浮动](#%E6%B5%AE%E5%8A%A8)
    - [1. 文本绕排图片](#1-%E6%96%87%E6%9C%AC%E7%BB%95%E6%8E%92%E5%9B%BE%E7%89%87)
    - [2. 创建分栏](#2-%E5%88%9B%E5%BB%BA%E5%88%86%E6%A0%8F)
    - [围住浮动元素的三种方法](#%E5%9B%B4%E4%BD%8F%E6%B5%AE%E5%8A%A8%E5%85%83%E7%B4%A0%E7%9A%84%E4%B8%89%E7%A7%8D%E6%96%B9%E6%B3%95)

<!-- /TOC -->

# 浮动

CSS 设计float 属性的主要目的，是为了实现文本绕排图片的效果。然而，这个属性居然也成了创建多栏布局最简单的方式。

## 1. 文本绕排图片

```css
<img …… />
<p>…the paragraph text…</p>
CSS 规则如下。
/*为简明起见，省略了字体声明*/
p {margin:0; border:1px solid red;}
/*外边距防止图片紧挨文本*/
img {float:left; margin:0 4px 4px 0;}
```

![](https://raw.githubusercontent.com/JayChenFE/css_review/master/Stylin_with_CSS/img/3-1.jpg)
>浮动非图片元素时，必须给它设定宽度，否则后果难以预料。图片无所谓，因为它本身有默认的宽度。

## 2. 创建分栏
```
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