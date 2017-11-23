
<!-- TOC -->

- [CSS背景属性](#css%E8%83%8C%E6%99%AF%E5%B1%9E%E6%80%A7)
    - [背景重复](#%E8%83%8C%E6%99%AF%E9%87%8D%E5%A4%8D)
    - [背景位置](#%E8%83%8C%E6%99%AF%E4%BD%8D%E7%BD%AE)
        - [背景位置的值](#%E8%83%8C%E6%99%AF%E4%BD%8D%E7%BD%AE%E7%9A%84%E5%80%BC)
    - [背景尺寸](#%E8%83%8C%E6%99%AF%E5%B0%BA%E5%AF%B8)
    - [背景粘附](#%E8%83%8C%E6%99%AF%E7%B2%98%E9%99%84)

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

![](https://raw.githubusercontent.com/JayChenFE/css_review/master/Stylin_with_CSS/img/4-3.png)  

**`background-position` 属性的默认值`top` `left`    VS    `center ` `center`**



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

  ​

- 使用关键字和百分比值时:

  设定的值同时应用于元素和图片。

  换句话说，如果设定了`33%` `33%` ，则图片水平`33%` 的位置与元素水平`33%` 的位置对齐。垂直方面也一样。

  ` center center` 则是把图片的中心点定位在了元素的中心点。

  ​

- 使用像素之类的绝对单位数时:

  图片的左上角会被放在距离元素左上角指定位置的地方。

  - 使用负值时,可以把图片的左上角定位到元素外部，从而在元素中只能看到部分图片。
  - 给图片设定足够大的正值，也可以把图片的右下角推到元素外部，从而在元素中也只能看到部分图片。

## 背景尺寸

`background-size` 是`CSS3 `规定的属性，但却得到了浏览器很好的支持:

![](https://raw.githubusercontent.com/JayChenFE/css_review/master/Stylin_with_CSS/img/4-5.png)

![](https://raw.githubusercontent.com/JayChenFE/css_review/master/Stylin_with_CSS/img/4-6.png)

`background-size`的取值:

- 50%：缩放图片，使其填充背景区的一半。
- 100px 50px：把图片调整到100 像素宽，50 像素高。
- cover：拉大图片，使其完全填满背景区；保持宽高比。
- contain：缩放图片，使其恰好适合背景区；保持宽高比。



![](https://raw.githubusercontent.com/JayChenFE/css_review/master/Stylin_with_CSS/img/4-7.png)

**给一个居中的不重复的背景图片应用不同的`background-size`  值的效果**

> 注意，别把本来很小的图片拉得太大，那样会导致图片质量失真。

## 背景粘附

`background-attachment `属性控制滚动元素内的背景图片是否随元素滚动而移动,取值为:

- `scroll` (默认值):背景图片随元素移动
- `fixed` : 背景图片不会随元素滚动而移

`background-attachment:fixed`  最常用于给`body`  元素中心位置添加淡色水印，让水印
不随页面滚动而移动。

## 简写背景属性

```css
body {
background-image:url(images/watermark.png);
background-position:center;
background-color:#fff;
background-repeat:no-repeat;
background-size:contain;
background-attachment:fixed;
}
```



等价于

```css
body {background:url(images/watermark.png) center #fff no-repeat contain fixed;}
```

声明中少写了哪个属性的值（比如没写no-repeat），就会使用相应属性的默认值（repeat）。

## 其他CSS3 背景属性

记得检测浏览器的支持情况

- `background-clip` 

  控制背景绘制区域的范围，比如可以让背景颜色和背景图片只出现在内容区，而不出现在内边距区域。

  默认情况下，背景绘制区域是扩展到边框外边界的。

  简单说就是如何剪切超出的部分。

  - 语法:

    ```css
    background-clip: border-box
    background-clip: padding-box
    background-clip: content-box
    background-clip: inherit
    ```

  - 取值:

    - `border-box`:

         背景延伸到边框外沿（但是在边框之下）。

    - `padding-box`

      边框下面没有背景，即背景延伸到内边距外沿。

    - `content-box`

      背景裁剪到内容区 (`content-box) `外沿。

  - 例子:

    - html

      ```html
      <p class="border-box">The yellow background extends behind the border.</p>
      <p class="padding-box">The yellow background extends to the inside edge of the border.</p>
      <p class="content-box">The yellow background extends only to the edge of the content box.</p>
      ```

    - css:

      ```css
      p {
         border: 5px navy;
         border-style: dotted double;
         margin: 1em;
         padding: 2em;
         background: #F8D575;
      }
      .border-box { background-clip: border-box; }
      .padding-box { background-clip: padding-box; }
      .content-box { background-clip: content-box; }
      ```

    - 结果

      ![](https://raw.githubusercontent.com/JayChenFE/css_review/master/Stylin_with_CSS/img/4-8.png)


      ![(https://raw.githubusercontent.com/JayChenFE/css_review/master/Stylin_with_CSS/img/4-8.png) 

- `background-origin`

  控制背景定位区域的原点，可以设定为元素盒子左上角以外的位置。

  比如，可以设定以内容区左上角作为原点。

- `background-break`

   控制分离元素（比如跨越多行的行内盒子）的显示效果。