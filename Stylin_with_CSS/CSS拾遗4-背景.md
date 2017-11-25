

<!-- TOC -->

- [CSS背景属性](#css%E8%83%8C%E6%99%AF%E5%B1%9E%E6%80%A7)
    - [背景重复](#%E8%83%8C%E6%99%AF%E9%87%8D%E5%A4%8D)
    - [背景位置](#%E8%83%8C%E6%99%AF%E4%BD%8D%E7%BD%AE)
        - [背景位置的值](#%E8%83%8C%E6%99%AF%E4%BD%8D%E7%BD%AE%E7%9A%84%E5%80%BC)
    - [背景尺寸](#%E8%83%8C%E6%99%AF%E5%B0%BA%E5%AF%B8)
    - [背景粘附](#%E8%83%8C%E6%99%AF%E7%B2%98%E9%99%84)
    - [简写背景属性](#%E7%AE%80%E5%86%99%E8%83%8C%E6%99%AF%E5%B1%9E%E6%80%A7)
    - [其他CSS3 背景属性](#%E5%85%B6%E4%BB%96css3-%E8%83%8C%E6%99%AF%E5%B1%9E%E6%80%A7)
        - [`background-clip`](#background-clip)
        - [`background-origin`](#background-origin)
        - [~~`background-break`~~](#background-break)
    - [多背景图片](#%E5%A4%9A%E8%83%8C%E6%99%AF%E5%9B%BE%E7%89%87)
        - [厂商前缀](#%E5%8E%82%E5%95%86%E5%89%8D%E7%BC%80)
    - [背景渐变](#%E8%83%8C%E6%99%AF%E6%B8%90%E5%8F%98)

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

### 背景位置的值

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

`background-attachment`属性控制滚动元素内的背景图片是否随元素滚动而移动,取值为:

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

### `background-clip` 

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

  - `border-box(默认值)`

       背景延伸到边框外沿（但是在边框之下）。

  - `padding-box`

    边框下面没有背景，即背景延伸到内边距外沿。

  - `content-box`

    背景裁剪到内容区 `(content-box)`外沿。

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

    ![](https://raw.githubusercontent.com/JayChenFE/css_review/master/Stylin_with_CSS/img/4-9.png)

### `background-origin`

控制背景定位区域的原点，可以设定为元素盒子左上角以外的位置。

比如，可以设定以内容区左上角作为原点。

- 语法:

  ```css
  background-origin: border-box
  background-origin: padding-box
  background-origin: content-box

  background-origin: inherit
  ```

- 取值:

  - `border-box`:

    背景图片的摆放以`border`区域为参考

  - `padding-box`

    背景图片的摆放以`padding`区域为参考

  - `content-box`

    背景图片的摆放以`content`区域为参考

- 例子:

  ```css
  /*例1*/
  .example {
     border: 10px double;
     padding: 10px;
     background: url('image.jpg');
     background-position: center left;
     /* 背景将在内容区padding内部填充 */ 
     background-origin: content-box;
  }

  /*例2*/
  #example2 {
      border: 4px solid black;
      padding: 10px;
      background: url('image.gif');
      background-repeat: no-repeat;
      background-origin: border-box;
   }

  /*例3*/
  div {
    background-image: url('logo.jpg'), url('mainback.png');
    background-position: top right, 0px 0px;
    background-origin: content-box, padding-box;
  }
  ```

### ~~`background-break`~~

~~控制分离元素（比如跨越多行的行内盒子）的显示效果。~~ 

## 多背景图片

  ```css
  p {
      height: 150px;
      width: 348px;
      border: 2px solid #aaa;
      margin: 20px auto;
      font: 24px/150px helvetica, arial, sansserif;
      text-align: center;
      background: url(images/turq_spiral.png) 30px -10px no-repeat,
      url(images/pink_spiral.png) 145px 0px no-repeat,
      /*为了防止图片加载失败时元素背景处于默认的透明状态，
        在最后一条声明中加上了背景颜色（#ffbd75）*/
      url(images/gray_spiral.png) 140px -30px no-repeat, #ffbd75;
  }
  ```
  ![](https://raw.githubusercontent.com/JayChenFE/css_review/master/Stylin_with_CSS/img/4-10.png)

  <center>**多张图片可以在背景中叠加起来，CSS 规则中先列出的图片在上层**</center> 

### 厂商前缀

为鼓励浏览器厂商尽早采用W3C 的CSS3 推荐标准，于是就产生了`VSP（Vendor Specific Prefixes，厂商前缀）` 的概念 

以`W3C` 推荐的`transform`  属性为例

```css
transform: skewX(-45deg);
```

**由于这个属性还没有完全定案**，为保证在大多数浏览器以及它们的实验性实现中能够使用这个属性，应该针对想要支持的浏览器为该属性添加VSP。每个浏览器只使用各自能理解的属性声明。

```css
-moz-transform:skewX(-45deg); /* Firefox */
-webkit-transform:skewX(-45deg); /* Chrome 及Safari */
-ms-transform:skewX(-45deg); /* 微软Internet Explorer */
-o-transform:skewX(-45deg); /* Opera */
transform:skewX(-45deg); /* 最后是W3C 标准属性 */
```

以下CSS3 属性必须加`VPS`：

```txt
border-image translate

linear-gradient transition

radial-gradient background*

transform background-image*

transform-origin

* 针对背景图片或渐变

```

## 背景渐变

  渐变就是在一定长度内两种或多种颜色之间自然的过渡,渐变分为两种:

- 线性渐变:从元素的一端延伸到另一端
- 放射性渐变:从元素内一点向四周发散

>渐变是CSS 帮我们生成的背景图片。添加渐变可以使用`background-image`   属性，也可以使用简写`background `属性。

下面是一个渐变的例子:

```html
<div class="gradient1"><h1>1</h1></div>
<div class="gradient2"><h1>2</h1></div>
<div class="gradient3"><h1>3</h1></div>
```

```css
* {
    margin: 0;
    padding: 0;
}

div {
    height: 150px;
    width: 200px;
    border: 1px solid #ccc;
    float: left;
    margin: 16px;
}


/* styles the element box 为元素盒子添加样式 */
/* centers the headline vertically and horizontally 标题垂直水平居中*/

h1 {
    text-align: left;
    font: 25px Helvetica, Arial, sans-serif;
    margin: 120px 5px;
}

/* top to bottom by default  默认为从上到下*/
.gradient1 {
    background: -webkit-linear-gradient(#e86a43, #fff);
}
/* left to right 从左到右*/
.gradient2 {
    background: -webkit-linear-gradient(left, #64d1dd, #fff);
}
/* top-left to bottom-right  左上到右下*/
.gradient3 {
    background: -webkit-linear-gradient(-45deg, #e86a43, #fff);
}

```

