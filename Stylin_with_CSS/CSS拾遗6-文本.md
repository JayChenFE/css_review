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

**如果你想缩进整个段落，可以使用段落的margin-left 属性**。换句话说，你得把整个包含盒子向右移动才行。而你永远要记住，文本属性只应用于这个长长的、细细的、内部的文本盒子，而不是包含元素的盒子。

> 请注意，在设定缩进和外边距时要使用em，以便在改变字体大小时，它们的长度能够按比例变化。