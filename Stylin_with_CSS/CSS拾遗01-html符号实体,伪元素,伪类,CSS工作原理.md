<!-- TOC -->

- [html符号实体](#html%E7%AC%A6%E5%8F%B7%E5%AE%9E%E4%BD%93)
- [伪类](#%E4%BC%AA%E7%B1%BB)
    - [伪类顺序](#%E4%BC%AA%E7%B1%BB%E9%A1%BA%E5%BA%8F)
- [伪元素](#%E4%BC%AA%E5%85%83%E7%B4%A0)
- [CSS工作原理](#css%E5%B7%A5%E4%BD%9C%E5%8E%9F%E7%90%86)
    - [继承](#%E7%BB%A7%E6%89%BF)
    - [层叠](#%E5%B1%82%E5%8F%A0)
        - [数字值](#%E6%95%B0%E5%AD%97%E5%80%BC)
    - [计算特指度](#%E8%AE%A1%E7%AE%97%E7%89%B9%E6%8C%87%E5%BA%A6)
        - [使用"ICE"公式计算三个值：](#%E4%BD%BF%E7%94%A8ice%E5%85%AC%E5%BC%8F%E8%AE%A1%E7%AE%97%E4%B8%89%E4%B8%AA%E5%80%BC%EF%BC%9A)
        - [层叠规则四：顺序决定权重](#%E5%B1%82%E5%8F%A0%E8%A7%84%E5%88%99%E5%9B%9B%EF%BC%9A%E9%A1%BA%E5%BA%8F%E5%86%B3%E5%AE%9A%E6%9D%83%E9%87%8D)
        - [简化版的层叠规则](#%E7%AE%80%E5%8C%96%E7%89%88%E7%9A%84%E5%B1%82%E5%8F%A0%E8%A7%84%E5%88%99)

<!-- /TOC -->

# html符号实体

[菜鸟教程-html符号实体](http://www.runoob.com/tags/html-symbols.html)
[HTML Named Special Symbols](http://turner.faculty.swau.edu/webstuff/htmlsymbols.html)
[Special Entities](http://htmlhelp.com/reference/html40/entities/special.html)

# 伪类

## 伪类顺序

口诀 `L`o`V`e,`HA`
参考:
[简书](http://www.jianshu.com/p/c7d766e9dfdd)
[CSDN](http://www.cnblogs.com/xiayi/p/5350423.html)

##:target 伪类
e:target
如果用户点击一个指向页面中其他元素的链接，则那个元素就是目标（target），可以
用:target 伪类选中它。
对于下面这个链接

```css
<a href="#more_info">More Information</a>
```

位于页面其他地方、ID 为more_info 的那个元素就是目标。该元素可能是这样的：
```css
<h2 id="more_info">This is the information you are looking for.</h2>
```
那么，如下CSS 规则
```css
#more_info:target {background:#eee;}
```
会在用户单击链接转向ID 为more_info 的元素时，为该元素添加浅灰色背景。
<br>
维基百科在其引证中大量使用了:target 伪类。维基百科的引证链接就是正文里那些
不起眼的数字链接。引证本身则位于长长的页面的最下方。如果没有:target 应用的
突出显示，很难知道你点击的链接对应着一大堆引证中的哪一个。

# 伪元素

1. ::first-letter 伪元素
    ```css
        e::first-letter
    ```
    比如，以下CSS 规则：
    ```css
    p::first-letter {font-size:300%;}
    ```
    >如果不用伪元素创建这个首字符放大效果，必须手工给该字母加上`<span>`标签，
    >然后再为该标签应用样式。而伪元素实际上是替我们添加了无形的标签。

    ![](https://raw.githubusercontent.com/JayChenFE/css_review/master/Stylin_with_CSS/img/1-1.jpg)

2. ::first-line 伪元素
    ```css
    e::first-line
    ```
    可以选中文本段落（一般情况下是段落）的第一行。例如
    ```css
    p::first-line {font-variant:small-caps;}
    ```
    可以把第一行以小型大写字母显示
    ![](https://raw.githubusercontent.com/JayChenFE/css_review/master/Stylin_with_CSS/img/1-2.jpg)
# CSS工作原理
## 继承
CSS 中有很多属性是可以继承的，其中相当一部分都跟文本有关，比如颜色、字体、字号。然而，也有很多CSS属性不能继承，因为继承这些属性没有意义。这些不能继承的属性主要涉及元素盒子的定位和显示方式，比如边框、外边距、内边距
<br>
假设我们想创建一个边栏，在其中放一组链接。为此，我们用nav元素嵌套该组链接，并给nav应用了一种字号和一个边框效果，比如2 像素宽的红色边框。不难想象，nav中的所有链接都继承它的字号很正常，可要是也继承它的边框就不合适了。当然，这些链接不会继承边框效果，因为border 属性不能继承。
<br>
由于字体和文本样式是可以继承的，所以在使用相对字体单位（如百分比和em）时要格外小心。如果某个标签的字体大小被设置为80%，而它的一个后代的字体大小也被设置为80%，那么该后代中文本最终的字体大小将是64%（80%的80%）。这有时候可能并不是你想要的结果
## 层叠
### 数字值
em 和ex 都是字体大小的单位，但在CSS 中，它们作为长度单位适用于任何元素。
先说说em ，它表示一种字体中字母M的宽度，因此它的具体大小取决于你使用的字体。
而ex 呢，等于给定字体中字母x 的高度（小写字母x 代表一种字体的字母中间部分的高度，不包括字母上、下突出的部分——如d 和p 上下都出头儿）。
百分比非常适合设定被包含元素的宽度，此时的百分比就是相对于宽度而言的.把HTML结构元素的宽度设定为body宽度的百分比，是“流式”设计的关键所在。
<br>
以下就是浏览器层叠各个来源样式的顺序：

1. 浏览器默认样式表
2. 用户样式表
3. 作者链接样式表（按照它们链接到页面的先后顺序）
4. 作者嵌入样式
5. 作者行内样式

## 计算特指度

### 使用"ICE"公式计算三个值：

I - C - E
ICE 并非真正的三位数，只不过大多情况下把结果看成一个三位数没有问题，三位数
最大的胜出。但是，千万得知道0-1-12 与0-2-0 相比，仍然是0-2-0 的特指度更高。
三个字母间的短横线是分隔符，并非减号。针对这个公式的计分办法如下：

1. 选择符中有一个ID，就在I 的位置上加1；
2. 选择符中有一个类，就在C 的位置上加1；
3. 选择符中有一个元素（标签）名，就在E 的位置上加1；
4. 得到一个三位数。

例子:

```css
p                                0-0-1 特指度=1
p.largetext                      0-1-1 特指度=11
p#largetext                      1-0-1 特指度=101
body p#largetext                 1-0-2 特指度=102
body p#largetext ul.mylist       1-1-3 特指度=113
body p#largetext ul.mylist li    1-1-4 特指度=114
```

在此，每个选择符都比前一个选择符的特指度更高。

### 层叠规则四：顺序决定权重

如果两条规则都影响某元素的同一个属性，而且它们的特指度也相同，则位置最靠下（或后声明）的规则胜出。

### 简化版的层叠规则

- 规则一：包含ID 的选择符胜过包含类的选择符，包含类的选择符胜过包含标签名的选择符。

- 规则二：如果几个不同来源都为同一个标签的同一个属性定义了样式，行内样式胜过嵌入样式，嵌入样式胜过链接样式。在链接的样式表中，具有相同特指度的样式，后声明的胜过先声明的。

>规则一胜过规则二。换句话说，如果选择符更明确（特指度更高），无论它在哪里，都会胜出。

- 规则三：设定的样式胜过继承的样式，此时不用考虑特指度（即显式设定优先）。
    下面简单解释一下规则三。比如下面的标记

    ```html
    <div id="cascade_demo">
    <p id="inheritance_fact">Inheritance is <em>weak</em> in the Cascade</p>
    </div>
    ```
    和下面的规则
    ```css
    div#cascade_demo p#inheritance_fact {color:blue;}
    ```
    2 - 0 - 2 （高特指度）    会导致单词“weak”变成蓝色，因为它从父元素p 那里继承了这个颜色值。但是，只要我们再给em 添加一条规则
    ```css
    em {color:red;}
    ```
    0 - 0 - 1 （低特指度）
    em 就会变成红色。因为，虽然它的特指度低（0-0-1），但em继承的颜色值，会被为它明确（显式）指定的颜色值覆盖，就算（隐式）遗传该颜色值的规则的特指度高（2-0-2）也没有用。
