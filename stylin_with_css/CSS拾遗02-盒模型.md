<!-- TOC -->

- [border](#border)
- [reset.css](#resetcss)
- [MFC](#mfc)
    - [什么是MFC](#%E4%BB%80%E4%B9%88%E6%98%AFmfc)
    - [为什么MFC](#%E4%B8%BA%E4%BB%80%E4%B9%88mfc)
    - [MFC的单位](#mfc%E7%9A%84%E5%8D%95%E4%BD%8D)
    - [盒子有多大](#%E7%9B%92%E5%AD%90%E6%9C%89%E5%A4%9A%E5%A4%A7)

<!-- /TOC -->

# border

边框（border）有3 个相关属性。

- 宽度（border-width）。可以使用thin、medium 和thick 等文本值，也可以使用除百分比和负值之外的任何绝对值。
- 样式（border-style）。有none、hidden、dotted、dashed、solid、double、groove、ridge、inset 和outset 等文本值。
- 颜色（border-color）。可以使用任意颜色值，包括RGB、HSL、十六进制颜色值和颜色关键字。

>border 的第四个属性border-radius 并不影响盒模型的定位

# reset.css

[Eric 为什么要写一个涉及面如此之广的重置样式表](http://meyerweb.com/eric/thoughts/2007/04/18/reset-reasoning)
[reset.css的下载地址](http://meyerweb.com/eric/tools/css/reset)

# MFC

## 什么是MFC

垂直外边距叠加（或者叫重叠），直到一个元素的外边距碰到另一个元素的边框为止
>注意啦，叠加的只是垂直外边距，水平外边距不叠加。对于水平相邻的元素，它们
>的水平间距是相邻外边距之和

例子:
假设有3 个段落，前后相接，而且都应用以下规则

```css
p {
    height: 50px;
    border: 1px solid #000;
    background-color: #fff;
    margin-top: 50px;
    margin-bottom: 30px;
}
```

由于第一段的下外边距与第二段的上外边距相邻，你自然会认为它们之间的外边距是80像素（50+30），但是你错啦！它们实际的间距是50 像素。
像这样上下外边距相遇时，它们就会相互重叠，直至一个外边距碰到另一个元素的边框。
就上面的例子而言，第二段较宽的上外边距会碰到第一段的边框。也就是说，较宽的外边距决定两个元素最终离多远，没错——50 像素。这个过程就叫外边距叠加。
![](https://raw.githubusercontent.com/JayChenFE/css_review/master/Stylin_with_CSS/img/2-1.jpg)

## 为什么MFC

如果有一连串段落都被应用了相同的样式，那么对其中第一段和最后一段来说，它们的上外边距和下外边距决定了它们与包含元素的间距。**<span style='color:red'>而那些位于中间的段落呢，根本不需要两个外边距加起来那么宽的间距**</span>。因此，上面例子所示的那样，相邻的外边距叠加起来是最合理的，哪个外边距宽，就以哪个外边距作为段间距。

## MFC的单位

根据经验，为文本元素设置外边距时通常需要混合使用不同的单位。比如说，一个段落的左、右外边距可以使用像素，以便该段文本始终与包含元素边界保持固定间距，不受字号变大或变小的影响。而对于上、下外边距，以em为单位则可以让段间距随字号变化而相应增大或缩小，比如：

```css
/*这里使用了简写属性把上、下外边距设置为.75em，把左、右外边距设置为30 像素*/
p {
    font-size: 1em;
    margin: .75em 30px;
}
```

>这样，段落的垂直间距始终会保持为字体高度的四分之三（上下外边距都是.75em，叠加后还是.75em）。
>
>如果用户增大了字号，那么不仅段落中的文本会变大，段间距也会成比例变大。
>
>这样，页面的整体布局就会比较协调一致。与此同时，使用像素单位的左、右外边距不会改变。
>
>这样字号变化不会影响到布局宽度

## 盒子有多大

没设定width时是auto

>盒模型结论一：没有（就是没有设置width的）宽度的元素始终会扩展到填满其父元素的宽度为止。添加水平边框、内边距和外边距，会导致内容宽度减少，减少量等于水平边框、内边距和外边距的和。
>
>
>盒模型结论二：为设定了宽度的盒子添加边框、内边距和外边距，会导致盒子扩展得更宽。**实际上，盒子的width属性设定的只是盒子内容区的宽度，而非盒子要占据的水平宽度。**

注意:
CSS3 新增了一个box-sizing 属性，通过它可以将有宽度的盒子也设定成具有默认的auto 状态下的为。