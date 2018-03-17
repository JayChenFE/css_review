# 文本属性

如果想缩进段落，实现$10^6$中的上角标效果，在标题字符间增加一些间距，以及其他一些排版效果，就要用到CSS 的
文本属性。

以下是几个最有用的CSS 文本属性：

- text-indent
- letter-spacing
- word-spacing
- text-decoration
- text-align
- line-height
- text-transform
- vertical-align

## 文本缩进(text-indent)

值：长度值（正、负均可）。
示例：

```css
p {text-indent:3em;}
```

示例:

```html
<p class="indent">This is example 1. This paragraph of text has an indent of 3 ems. Because its value is positive (greater than 0), all the text stays within the element. Things get more complicated if I start using negative margins to make the first line "outdent" instead.</p>
<p class="outdent_wrong">This is example 2. This paragraph of text has a negative indent. Because this element does not have enough space to its left, the hanging text is clipped by the edge of the browser window. The border of this element is displayed to help you see the nature of the problem.</p>
<p class="outdent_right">This is example 3. This paragraph of text has the same negative indent as the example above, but because this element has a left margin value greater than the negative indent value, the hanging text is not clipped by the edge of the browser window. The border of this element is displayed to help you see how a potential problem is avoided.</p>
 <p class="outdent_right2">This is example 4. Here is the same styling as the previous paragraph, but without the element border so you can clearly see the effect. Indents provide a visual indication of the start of paragraphs when you don't want to use space to separate them.</p>
 <p class="outdent_right2">Here is a second paragraph with no space between it and the previous one. The negative value indent makes it clear that this is a new paragraph. Positive value indents can serve the same purpose.</p>
```

```css
/* font-size:120%; */
body {font-family:helvetica, arial, sans-serif; font-size:1em;}
p.indent {border:1px solid red; line-height: 1.1; text-indent:3em;}
p.outdent_wrong {border:1px solid red; line-height: 1.1; text-indent:-1.5em;}
p.outdent_right {border:1px solid red; line-height: 1.1; text-indent:-1.5em; margin-left:1.65em;}
p.outdent_right2 {line-height: 1.1; text-indent:-1.5em; margin:0 0 0 1.65em;}
```

![](https://raw.githubusercontent.com/JayChenFE/css_review/master/Stylin_with_CSS/img/6-1.png)

> `text-indent` 是可以被子元素继承的,继承的是计算的值
>
> 假设有一个400 像素宽的div，包含的文本缩进5%，则缩进的距离是20 像素（400 的5%）。
> 在这个div 中有一个200 像素宽的段落。作为子元素，它继承父元素的text-indent 值，所以它包含的文本也缩进。但继承的缩进值是多少呢？不是5%，而是20 像素

### 文本之“蛇”

CSS 会把元素中的文本放在一个不可见的盒子里，比如对p 元素中的一段文本，CSS 将其视为很长的一行，只不过在遇到容器边界时会折行

```html
<style type="text/css">
body {
    font-family: helvetica, arial, sans-serif;
    font-size: 1em;
}

p {
    border: 3px solid red;
    line-height: 1.7;
    padding: 4px;
    text-indent: 10px;
}

span {
    border: 1px solid green;
}
</style>
</head>

<body>
    <p><span>Here is a long paragraph of text. Think of it as a long, thin snake contained within the paragraph's box. 
    The paragraph element contains the text, but CSS also applies a box around the text itself, and it is this inner box to which the text properties are applied. 
    In this example, the containing element's box is in red and the inner box around the text is in green. As you can see from the way the inner box is drawn, 
    CSS sees the text as one long strip, even though the width of the container causes it to be broken across several lines.</span></p>
    <!--end footer-->
</body>
```

![](https://raw.githubusercontent.com/JayChenFE/css_review/master/Stylin_with_CSS/img/6-2.png)

这里的文本盒子跨行时是断开的，只有第一行开头和最后一行末尾是封闭的。使用文本属性`text-indent` （缩进的是这个文本盒子的起点位置。

**后续的行是不会缩进的，因为在CSS 看来，它们就是一个整体。**

**如果想缩进整个段落，可以使用段落的margin-left 属性**。换句话说，你得把整个包含盒子向右移动才行。而你永远要记住，文本属性只应用于这个长长的、细细的、内部的文本盒子，而不是包含元素的盒子。

> 请注意，在设定缩进和外边距时要使用`em` ，以便在改变字体大小时，它们的长度能够按比例变化。

## 字符间距(letter-spacing)

值：任何长度值（正、负值均可）。
示例：

```css
p {letter-spacing:.2em;}
```

> 默认的字符间距在字体变大时会使文本显得松散，因此缩小大标题的字距可以让网页显得更专业

## 单词间距(word-spacing)

值：任何长度值（正、负值均可）
示例：p {word-spacing:.2em;}

> 纯汉字文本一段之中没有空格，因此`word-spacing` 对中文网页几乎没有用，但对中英混排段落可能有用;`letter-spacing` 对英文字母、汉字及其他字符都起作用

### 文本装饰

值：

- underline
- overline
- line-through
- blink
- none

示例：

```css
.retailprice {text-decoration:line-through;}
```

![](https://raw.githubusercontent.com/JayChenFE/css_review/master/Stylin_with_CSS/img/6-3.png)

文本装饰最主要的应用是控制链接的下划线.下面这个例子展示了怎么通过`text-decoration` 去掉导航条中链接的下划线

```css
nav a {text-decoration:none;}
a:hover {text-decoration:underline;}
```

## 文本对齐

值：

- left 左对齐
- right 右对齐
- center 居中
- justify 两端对齐

示例：

```css
p {text-align:right;}
```

## 行高

值：任何数字值（不用指定单位）

示例：

```css
p {line-height:1.5;}
```

CSS 中的行高平均分布在一行文本的上方和下方。举个例子，如果字体大小是12 像素，行高是20 像素，则浏览器会在文本上方和下方各加4 像素的空白，以凑足20像素的行高

修改默认行高最简单的方式就是使用font 快捷属性，以复合值的形式把font-size 和line-height 值写在一块，比如：

```css
div#intro {font:1.2em/1.4 helvetica, arial, sans-serif;}
```

注意这里不用给`line-height` 值指定单位，只要一个数值就可以。此时，浏览器会用计算得到的1.2em 的像素数乘以1.4，结果就是行高

## 文本转换

值：

- none 默认值
- uppercase
- lowercase
- capitalize 每个词的首字母转换为大写

示例：

```css
p {text-transform:capitalize;}
```

> 要想实现小型大写字母的首字母放大效果，可以再加上`font-variant:small-caps`声明 

## 垂直对齐

值：

- 任意长度值
- sub
- super
- top
- middle
- bottom 

示例：

```css
span {vertical-align:60%;}
```

`vertical-align`  以**基线为参照**上下移动文本，但这个属性**只影响行内元素**

如果想在垂直方向上对齐块级元素，必须把其`display` 属性设定为`inline` 。

`vertical-align` 属性最常用于公式或化学分子式中的上标和下标，比如$x^4-y^5 $或$N_3O$  

```html
<style type="text/css">
body {
    font-family: helvetica, arial, sans-serif;
    font-size: 100%;
    background-color: #FFF;
}

h4 {
    margin: 1.4em 20px .5em;
    color: #069;
}

p {
    margin: 0 20px;
}

p.custom sub {
    vertical-align: -.4em;
    font-size: 60%;
}

p.custom sup {
    vertical-align: .65em;
    font-size: 65%;
}

p.customsmall {
    font-size: .8em;
    vertical-align: 1em
}

code {
    font-size: 1.35em;
}
</style>
</head>

<body>
    <h4>Default <code>sub</code> and <code>sup</code> styles</h4>
    <p>Enjoy mountain spring H<sub>2</sub>O. It's 10<sup>5</sup> times better than tap<sup>&dagger;</sup> water!</p>
    <p class="customsmall"><sup>&dagger;</sup><em>This means water provided through a municipal distribution system</em></p>

    <h4>Custom <code>sub</code> and <code>sup</code> styles</h4>
    <p class="custom">Enjoy mountain spring H<sub>2</sub>O. It's 10<sup>5</sup> times better than tap<sup>&dagger;</sup> water!</p>
    <p class="customsmall"><sup>&dagger;</sup><em>This means water provided through a municipal distribution system</em></p>
</body>

```

![](https://raw.githubusercontent.com/JayChenFE/css_review/master/Stylin_with_CSS/img/6-4.png)

> 虽然HTML 标签<sup> 和<sub> 有默认的上标和下标样式， 但重新设定一下`vertical-align` 和`font-size`  属性能得到更美观的效果。

