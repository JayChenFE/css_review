# 字体来源

网页中的字体有三个来源

- 用户机器中安装的字体

- 保存在第三方网站上的字体

  最常见的是`Typekit`和`Google`，可以使用`link`  标签把它们链接到你的页面上

- 保存在你的`Web 服务器` 上的字体

  这些字体可以使用`@font-face`  规则随网页一起发送给浏览器

# 字体属性

- font-family
- font-size
- font-style
- font-weight
- font-variant
- font（简写属性）

> 字体 VS  文本
>
> `字体` 是“文字的不同体式”或者“字的形体结构”
>
> ​	对于英文而言，每种字体都是由一组具有独特样式的字母、数字和符号组成的。<br>	根据外观，字体可以分为不同的`类别（fontcollection）` ，包括:
>
> - 衬线字体（serif）、
>
> - 无衬线字体（sans-serif）
>
> - 等宽字体（monospace）
>
>   ​
>
>   每一类字体可以分成不同的字体族（font family），比如Times 和Helvetica。
>
>   ​
>
>   而字体族中又可以包含不同的 	字型（font face），反映了相应字体族基本设计的不同变化<br>例如`Times	Roman`、`Times Bold`、`Helvetica Condensed `和  `Bodoni italic` 。
>
> `文本` 就是一组字或字符，比如章标题、段落正文等等，跟使用什么字体无关。
>
> CSS 为字体和文本分别定义了属性
>
> `字体属性` 主要描述一类字体的大小和外观。比如，使用什么字体族`（是Times，还是Helvitica）` ，多大字号，粗体还是斜体。
>
> `文本属性` 描述对文本的处理方式。比如，行高或者字符间距多大，有没有下划线和缩进
>
>  如果你想让文字加粗，或者变斜体，可以设定字体属性。<br> 而行高和缩进这种只有对文本块（比如标题和段落）才有意义的样式，则要使用文本属性设定。

## 字体族（font-family）

`font-family`  用于设定元素中的文本使用什么字体。一般来说，应该给整个页面设定
一种主字体，然后只对那些需要使用不同字体的元素再应用`font-family` 

`font-family`  是可以继承的属性，因此它的值会遗传给所有后代元素

>据测试，`font-family` 的值（字体名）不区分大小写。但是，你可不能修改`Google` 或其他在线字体库生成的字体名，否则很可能无法使用它们提供的定制字体

### 字体栈

在指定文本的字体时，需要多列出几种后备字体，以防第一种字体无效。这个字体的列表也叫字体栈。

```css
/*如果字体名像Trebuchet MS 一样多于一个单词（有空格），应该加上引号。*/
body {font-family:"trebuchet ms", tahoma, sans-serif;}
```

给`font-family` 字体栈的最后一项指定通用字体类非常重要，比如`serif`、`sans-serif`，这是一种最保险的方法。

#### 常见的通用的字体类

- `serif`，也就是衬线字体，在每个字符笔画的末端会有一些装饰线 
- `sans-serif`，也就是无衬线字体，字符笔画的末端没有装饰线 
- `monospace`，也就是等宽字体，顾名思义，就是每个字符的宽度相等（也称代码体 ）
- `cursive`，也就是草书体或手写体 
- `fantasy` ，不能归入其他类别的字体（一般都是奇形怪状的字体）

`Verdana` 的后备用`Tahoma` 最好，因它们的“x 高度”相同。

```css
verdana, tahoma, sans-serif
```

如果想设定一个相对轻爽一点的无衬线字体，可以使用这个字体栈：

```css
helvetica, arial, sans-serif
```

关于如何选择字体的文章：http://unitinteractive.com/blog/2008/06/26/better-css-font-stacks/。

例子:

```css
{font-family:"hoefler text", georgia, times, serif;}
```

第一款字体是用户可能没有的,要在字体栈后面补上那些大多数操作系统都会内置的字体，比如这里的`georgia`、`times`，最后别忘了通用字体类`serif`。 

![](https://raw.githubusercontent.com/JayChenFE/css_review/master/Stylin_with_CSS/img/5-1.png)

## 字体大小(font-size)

`font-size`  是可以继承的。换句话说，改变一个元素的字体大小，可能会导致其子元素字体大小成比例地变化

浏览器样式表在设定所有元素的字体大小时，使用的都是相对单位`em`。比如，`h1` 被设定为`2em`，`h2 `是`1.5em`，`p` 是`1em`。**默认情况下，1em等于16 像素，这也是`font-size` 的基准大小**。换算成绝对值，h1 就是32 像素，h2是24 像素，p 是16 像素。

设定字体大小有绝对字体大小和相对字体大小两种方法

- 绝对字体大小

  像素、派卡（pica）或英寸是绝对单位，因此设定多大就多大，与祖先元素的字体大小无关

  >设定绝对字体大小时，也可以使用关键字值，比如x-small、medium、x-large，等等。其中，medium 等于基准大小，其他关键字要么小一点，要么大一点。关键字值涵盖的范围太窄，所以使用不广泛，，可以看看这篇文章：http://css-discuss.incutio.com/wiki/Using_Keywords

- 相对字体大小

  如果你给某个元素设定了相对字体大小，则该元素的字体大小要相对于**最近的“被设定过字体大小的”**祖先元素来确定。

  例如:

  ```html
  <body>
  <p>This is <strong>very important!</strong></p>
  </body>
  ```

  ```css
  p {font-size:.75em;}
  strong {font-size:.75em;}
  ```

  >想使用em，但又需要设定具体的像素大小，可以把body 的font-size 设定为62.5%。这样，就等于把基准大小从16 像素改为10 像素（16×62.5%=10）。然后，em 与像素的对应关系就十分明确了，比如1em 等于10 像素，1.5em 等于15 像素，2em 等于20 像素，等等

- rem

## 字体样式(font-style)

值:

- italic
- oblique
- normal

`font-style` 的作用仅仅是通过`italic` 把正体设为斜体，或者通过`normal` 把斜体设为正体.用oblique 代替italic 的结果 也一样. 

## 字体粗细

可能的值：100、200……900，或者lighter、normal、bold 和bolder。

对于`font-weight` 属性来说，最好只用`bold` 和`normal ` 这两个值

## 字体变化

值：small-caps、normal

small-caps会导致所有小写英文字母变成小型大写字母

## 简写字体属性

示例：

```html
<p>Here's a piece of text loaded up with every possible font property.</p>
```

```css
p {font: bold italic small-caps .9em helvetica, arial, sans-serif;}
```



<center>**一条声明指定字体加粗、斜体、小型大写字母、大小和字体族**</center>


