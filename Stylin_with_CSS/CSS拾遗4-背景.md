
<!-- TOC -->

- [CSS背景属性](#css%E8%83%8C%E6%99%AF%E5%B1%9E%E6%80%A7)
    - [背景重复](#%E8%83%8C%E6%99%AF%E9%87%8D%E5%A4%8D)

<!-- /TOC -->

![](https://raw.githubusercontent.com/JayChenFE/css_review/master/Stylin_with_CSS/img/4-1.png)

# CSS背景属性

- background-color
- background-image
- background-repeat
- background-position
- background-size
- background-attachment
- background（简写属性）
- background-clip、background-origin、background-break（目前尚未得到广泛支持）

## 背景重复

background-repeat 属性有4 个值。

- 默认值就是repeat
- repeat-x
- repeat-y
- no-repeat

![](https://raw.githubusercontent.com/JayChenFE/css_review/master/Stylin_with_CSS/img/4-2.png)

，CSS3 还规定另外两个值（但尚未得到浏览器支持），以控制背景图片重复确切的次数，即所有图片都是完整的，不会出现半张图片的现象。

- background-repeat:round：为确保图片不被剪切，通过调整图片大小来适应背景区域。
- background-repeat:space，为确保图片不被剪切，通过在图片间添加空白来适应背景区域。

## 背景位置

`background-position`  属性有5个关键字值，分别是

- top
- left
- bottom
- right 
- center

这些关键字中的**任意两个组合**起来都可以作为该属性的值

`background-position` 属性同时设定元素和图片的原点。

原点决定了元素和图片中某一点的水平和垂直坐标。

默认情况下，`background-position` 的原点位于左上角。

只给`background-position` 设定一个关键字值，则另一个也会取相同的值:

```css
/*center center 的简化写法*/
p#center {background-position:center;}
```



`background-position` 属性的默认值`top` `left`  VS `center ` `center`

![](https://raw.githubusercontent.com/JayChenFE/css_review/master/Stylin_with_CSS/img/4-3.png)

`background-position:center center` 设定图片中心点与元素中心点重合,以段落的中心点为起点，然后再向各个方向重复

通过把`background-position` 设定为`50%`和 `50`%，把`background-repeat` 设定为`no-repeat` ，实现了图片在背景区域内居中的效果:

```css
div {
height:150px;
width:250px;
border:2px solid #aaa;
margin:20px auto;
background-image:url(images/turq_spiral_150.png);
background-repeat:no-repeat;
background-position:50% 50%;
}
```

![](https://raw.githubusercontent.com/JayChenFE/css_review/master/Stylin_with_CSS/img/4-4.png)

###  背景位置的值

设定背景位置时可以使用三种值：

- 关键字

- 百分比

- 绝对或相对单位的数值

可以使用两个值分别设定水平和垂直位置。关键字指的顺序不重要，`left bottom`和`bottom left`  意思相同。

> 为了设定的值在所有浏览器中都有效，最好不要混用关键字值与数字值。

- 使用数值（比如`40%` `30%` ）时:

  第一个值表示水平位置，第二个值表示垂直位置。要是只设定一个值，则将其用来设定水平位置，而垂直位置会被设为`center` 。

在使用关键字和百分比值的情况下，设定的值同时应用于元素和图片。换句话说，如果设定了
33% 33%，则图片水平33%的位置与元素水平33%的位置对齐。垂直方面也一样。图3-37 所
示也是一个例子，那是通过center center 把图片的中心点定位在了元素的中心点。
像素之类的绝对单位数值就不一样了。要是用像素单位来设定位置，那么图片的左上角会被放
在距离元素左上角指定位置的地方。
有意思的是，还可以使用负值。这样就可以把图片的左上角定位到元素外部，从而在元素中只
能看到部分图片。当然，给图片设定足够大的正值，也可以把图片的右下角推到元素外部，从
而在元素中也只能看到部分图片。位于元素外部的那部分图片不会显示。