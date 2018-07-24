[TOC]

<!-- TOC -->

- [SASS基础教程](#sass基础教程)
  - [一、基本特性](#一基本特性)
  - [二、快速入门](#二快速入门)
    - [2.1 语法](#21-语法)
      - [2.1.1](#211)
      - [2.1.2 引用@import](#212-引用import)
    - [2.2 注释](#22-注释)
    - [2.3 变量](#23-变量)
      - [2.3.1 普通变量](#231-普通变量)
      - [2.3.2 默认变量](#232-默认变量)
      - [2.3.3 特殊变量](#233-特殊变量)
      - [2.3.4 多值变量](#234-多值变量)
      - [2.3.5 变量机制](#235-变量机制)
  - [三、CSS扩展](#三css扩展)
    - [3.1 选择器嵌套](#31-选择器嵌套)
    - [3.2 &引用父选择器](#32-引用父选择器)
    - [3.3 属性嵌套](#33-属性嵌套)
    - [3.4 跳出嵌套](#34-跳出嵌套)
    - [3.5 @mixin](#35-mixin)
    - [3.6 placeholder](#36-placeholder)
      - [3.6.1](#361)
      - [3.6.2 placeholder的特点](#362-placeholder的特点)
      - [**3.6.3 mixin VS placeholder**](#363-mixin-vs-placeholder)
  - [四 、SASS编程规范](#四-sass编程规范)
    - [4.1 语法格式](#41-语法格式)
      - [4.1.1 字符串](#411-字符串)
      - [4.1.2 数值](#412-数值)
      - [4.1.3  颜色](#413--颜色)
      - [4.1.4 列表 list](#414-列表-list)
      - [4.1.5 map](#415-map)
      - [4.1.6 混合宏@mixin](#416-混合宏mixin)
      - [4.1.7 继承](#417-继承)
      - [4.1.8  函数](#418--函数)
      - [4.1.9 参数列表](#419-参数列表)
      - [4.1.10  条件语句](#4110--条件语句)
      - [4.1.11  循环语句](#4111--循环语句)
    - [4.2 命名约定](#42-命名约定)
      - [4.2.1 常量](#421-常量)
      - [4.2.2响应式设计](#422响应式设计)
    - [4.3 命名空间](#43-命名空间)
    - [4.4 组织架构](#44-组织架构)

<!-- /TOC -->

# SASS基础教程  

SASS是最早、最成熟的CSS预处理，它可以通过变量、嵌套、函数、继承等使CSS变得更强大，更优雅，而且完全兼容CSS的语法。  

## 一、基本特性

- 完全兼容CSS3
- 诸如变量、嵌套、混合（`Mixins`）之类的语言扩展
- 操作颜色和其他的巨量实用函数
- 类似控制语句的强大特性
- 可以自定义的、格式良好的输出
- 整合Firebug  

## 二、快速入门  

### 2.1 语法  

#### 2.1.1

 SASS允许有两种语法

一种叫做`SCSS(Sassy CSS)`,使用`.scss`作为扩展名，它继承了`CSS3`的语法，一个验证合格的`CSS`样式表同样也是一个完全合格的`SCSS`样式表，同时具备相同的含义，而且`SCSS`能很好的识别大部分的`CSS Hacks`、浏览器厂商语法（例如老版本`IE`的滤镜）。  

另一种是比较早的语法，我们叫做缩进语法(使用`.SASS`作为扩展名，有时叫做`SASS`)提供了一种简洁书写`CSS`的语法，使用缩进而不是括号来代表嵌套，使用新行而不是分号分割属性，书写容易、代码简洁是很多人的最爱。

```scss
/* 1.使用SCSS */
$baseFontsize:14px;
$largeFontsize:16px;

body{
	font-size:$baseFontsize;
	p{
		font-size:$largeFontsize;
	}
}

/* 2.使用SASS*/
$baseFontsize: 14px
$largeFontsize: 16px

body
  font-size: $baseFontsize
  p
font-size: $largeFontsize
```

#### 2.1.2 引用@import

使用下划线命名的文件比如`_variables.scss`，`sass`称为局部文件。这个不是`css`中的`import`，`css`中的`import`指令有两大弊端：

- 必需放在文件行首；
- 只有执行到对应行中才加载。


### 2.2 注释

`sass`有两种注释方式，一种是标准的`css` 注释方式/* */，另一种则是//双斜杆形式的单行注释，不过这种单行注释不会被转译出来。

```scss
/*
*我是css的标准注释
*设置body内距
*/
body{
  padding:5px;
} 

//我是双斜杠表示的单行注释
//单行注释不会输出到生成的css文件中
//设置body内距
body{
  padding:5px; //5px
} 
```

### 2.3 变量  

sass的变量必须是$开头，后面紧跟变量名，而变量值和变量名之间就需要使用冒号(:)分隔开，如果值后面加上!default则表示默认值。   

#### 2.3.1 普通变量  

```scss
$fontSize: 12px;
body{
	font-size:$fontSize;
}
```

#### 2.3.2 默认变量  

```scss
$baseLineHeight:1.5 !default;//在变量值后面加上!default
body{
	line-height: $baseLineHeight; 
}

//sass的默认变量一般是用来设置默认值，然后根据需求来覆盖的，覆盖的方式也很简单，只需要在默认变量之前重新声明下变量即可
$baseLineHeight:2;
$baseLineHeight:1.5 !default;
body{
	line-height: $baseLineHeight; 
}
```

#### 2.3.3 特殊变量

一般我们定义的变量都为属性值，可直接使用，但是如果变量**作为属性或在某些特殊情况**下等则必须要以`#{$variables}`形式使用

```scss
$borderDirection:   top !default; 
$baseFontSize:  12px !default;
$baseLineHeight:1.5 !default;

//应用于class和属性
.border-#{$borderDirection}{
  	border-#{$borderDirection}:1px solid #ccc;
}

//应用于复杂的属性值
body{
	font:#{$baseFontSize}/#{$baseLineHeight};
}

//********************编译输出********************

.border-top{
  border-top:1px solid #ccc;
}

body {
  font: 12px/1.5;
}
```

#### 2.3.4 多值变量  

多值变量分为`list`类型和`map`类型，简单来说`list`类型有点像`js`中的数组，而`map`类型有点像`js`中的对象，`list`数据可通过空格、逗号或小括号分隔多个值。

```scss
//list类型
$linkColor: #08c #333 !default;//第一个值为默认值，第二个鼠标滑过值
a{
  color:nth($linkColor,1);

  &:hover{
    color:nth($linkColor,2);
  }
}

//********************编译输出********************

a{
  color:#08c;
}

a:hover{
  color:#333;
}
```

```scss
//map类型
$headings: (h1: 2em, h2: 1.5em, h3: 1.2em);
 @each $header, $size in $headings {
    # {
        $header
    }
    {
        font-size: $size;
    }
}

//********************编译输出********************
	
h1 {
    font-size: 2em;
}
h2 {
    font-size: 1.5em;
}
h3 {
    font-size: 1.2em;
}
```

#### 2.3.5 变量机制

在选择器中声明的变量会覆盖外面全局声明的变量。(这也就人们常说的`sass`没有局部变量)

```scss
$fontSize:  12px;
body{
	$fontSize: 14px;
	font-size:$fontSize;
}
p{
	font-size:$fontSize;
}

//********************编译输出********************

body{
	font-size:14px;
}
p{
	font-size:14px;
}
```


## 三、CSS扩展  

### 3.1 选择器嵌套  

`SASS`允许使用嵌套来减少父对象的重复，同时提高代码的可读性

```scss
#main p {
    color: #00ff00;
    width: 97%;
    .redbox {
        background-color: #ff0000;
        color: #000000;
    }
}

//********************编译输出********************

#main p {
  color: #00ff00;
  width: 97%;
}

#main p .redbox {
  background-color: #ff0000;
  color: #000000;
}
```

### 3.2 &引用父选择器 

在嵌套代码中使用父对象的引用有的时候是非常有用而且必要的，例如，当你给hover状态指定样式，或是给有特定类的body元素指定样式时，使用&引用父对象将会很高效。 

``` scss
a {
    font-weight: bold;
    text-decoration: none;
    &:hover {
        text-decoration: underline;
    }
    body.firefox & {
        font-weight: normal;
    }
}

//********************编译输出******************** 

a {
    font-weight: bold;
    text-decoration: none;
}
a:hover {
    text-decoration: underline;
}
body.firefox a {
    font-weight: normal;
}
```
### 3.3 属性嵌套

CSS里面有一些属性具有命名空间，例如`font-family`，`font-size`，`font-weight`等都在`font`的命名空间内，在CSS里如果你想声明一大堆这样的相同命名空间的属性，你需要一个个地重复写出来。SASS提供了一个解决方法，你只需要写一遍命名空间，然后进行子属性嵌套声明。  

```scss
.fakeshadow {
    border: {
        style: solid;
        left: {
            width: 4px;
            color: #888;
        }
        right: {
            width: 2px;
            color: #ccc;
        }
    }
}

//********************编译输出********************

.fakeshadow {
  border-style: solid;
  border-left-width: 4px;
  border-left-color: #888;
  border-right-width: 2px;
  border-right-color: #ccc; 
}
```

### 3.4 跳出嵌套

sass3.3.0中新增的功能，用来跳出选择器嵌套的。默认所有的嵌套，继承所有上级选择器，但有了这个就可以跳出所有上级选择器。

```scss
//没有跳出 
.parent-1 {
    color:#f00;
    .child {
        width:100px;
    }
}
//单个选择器跳出 
.parent-2 {
    color:#f00;
    @at-root .child {
        width:200px;
    }
}
//多个选择器跳出 
.parent-3 {
    background:#f00;
    @at-root {
        .child1 {
            width:300px;
        }
        .child2 {
            width:400px;
        }
    }
}

//********编译输出********

.parent-1 {
  color: #f00;
}
.parent-1 .child {
  width: 100px;
}

.parent-2 {
  color: #f00;
}
.child {
  width: 200px;
}

.parent-3 {
  background: #f00;
}
.child1 {
  width: 300px;
}
.child2 {
  width: 400px;
}
```

默认`@at-root`只会跳出选择器嵌套，而不能跳出`@media`或`@support`

如果要跳出这两种，则需使用`@at-root (without: media)`，`@at-root (without: support)`。

这个语法的关键词有四个：

- all（表示所有）

- rule（表示常规css）

- media（表示media）

- support（表示support，因为@support目前还无法广泛使用，所以在此不表）

我们默认的@at-root其实就是`@at-root (without:rule)`。

```scss
//跳出父级元素嵌套 
@media print {
    .parent1 {
        color: #f00;
        @at-root .child1 {
            width: 200px;
        }
    }
}

//跳出media嵌套，父级有效 
@media print {
    .parent2 {
        color: #f00;
        @at-root (without: media) {
            .child2 {
                width:200px;
            }
        }
    }
}

//跳出media和父级 
@media print {
    .parent3 {
        color: #f00;
        @at-root (without: all) {
            .child3 {
                width:200px;
            }
        }
    }
}

// ********************编译输出********************
@media print {
    .parent1 {
        color: #f00;
    }
    .child1 {
        width: 200px;
    }
}

@media print {
    .parent2 {
        color: #f00;
    }
}

.parent2 .child2 {
    width: 200px;
}

@media print {
    .parent3 {
        color: #f00;
    }
}

.child3 {
    width: 200px;
}
```


​	

`@at-root`与`&`配合使用  

```scss
.child {
    @at-root .parent & {
        color: #f00;
    }
}

//********************编译输出********************
.parent .child {
    color: #f00;
}
```

应用于`@keyframe`

```scss
.demo {
    //... 
    animation: motion 3s infinite;
    @at-root {
        @keyframes motion {
            ...
        }
    }
}

//********************编译输出******************** 
.demo {
    //...
    animation: motion 3s infinite;
}

@keyframes motion {
    //...
}
```

### 3.5 `@mixin`

Mixins允许自己定义样式，这些样式可以在全局样式表里重用，而不用去借助一些无语义的类，比如.float-left。Mixins可以包含完整的CSS样式规则和其他Sass中的特性规则等。mixin还可以接收参数，不同的参数值将产生不同的样式规则。

在样式表中，你会见到一些CSS规则声明被重复出现了好多次。你明白这样的代码不好，而且还知道DRY（Don't Repeat yourself）这个概念原则。现在使用`mixin`去改善这样的代码：

```scss
@mixin center() {
    display: block;
    margin-left: auto;
    margin-right: auto;
}

.container {
    @include center();
    /* Other styles here... */
}

/* Other styles... */

.image-cover {
    @include center;
}
```

### 3.6 `placeholder`  

#### 3.6.1 

`placeholder`是一种奇怪的东西。它们是class，但是在Sass编译过后，并不会被输出，出现在样式表文件里。
事实上，如果不是为了`@extend`这个指令，它都没什么意义。你可以这样去写一个`placeholder`:  

```scss
%center {
    display: block;
    margin-left: auto;
    margin-right: auto;
}
```

#### 3.6.2 placeholder的特点  

- placeholder的写法使用`%`，而不是.(点)，但是遵守class的命名规则。
- 如果编译Sass文件，placeholder的代码不会出现在生成的css的文件里。
- placeholder 要通过@extend 去使用。@extend指令的作用是继承一个CSS选择器的属性或者一个Sass的`placeholder`代码。  

#### **3.6.3 `mixin` VS `placeholder`**

`%(placeholder)`与`@mixin`的区别： 

- `@mixin`可以传递参数，而`%`不行；
- `@mixin`的调用方式是`@include`，而`%`的调用方式是`@extend`；
- `@include`产生的样式是以复制拷贝的方式存在的，
- `@extend`产生的样式是以组合声明的方式存在的。

如果你需要参数变量，使用`mixin`。否则，继承一个`placehodler`。这样做两个原因：

第一，在`placeholder`里面，不能像`mixin`那样传递使用参数变量。但是可以使用全局变量。  
第二，当你使用`mixin`时，Sass会重复输出这个`mixin`的属性规则内容，不会让CSS选择器公用这个`mixin`。这样的话，样式表将会变得很大。  
    
```scss
//使用mixin
@mixin center {
    display: block;
    margin-left: auto;
    margin-right: auto;
}

.container {
    @include center;
}

.image-cover {
    @include center;
}

//********************编译输出******************** 
.container {
    display: block;
    margin-left: auto;
    margin-right: auto;
}

.image-cover {
    display: block;
    margin-left: auto;
    margin-right: auto;
}

//使用placeholder
%center {
    display: block;
    margin-left: auto;
    margin-right: auto;
}

.container {
    @extend %center;
}

.image-cover {
    @extend %center;
}

// ********************编译输出******************** .container,
.image-cover {
    display: block;
    margin-left: auto;
    margin-right: auto;
}
```

使用`placeholder`可以避免重复相同的规则，会减少整个样式文件的大小。另外，如果你在不同的地方都要使用一些属性，但是这些属性的值是变量决定的，那么`mixin`是一个好的选择。如果你的CSS属性同时有固定的和变动的值，那么你可以组合使用`mixin`和`placeholder`。 

```scss
%center {
    margin-left: auto;
    margin-right: auto;
    display: block;
}

@mixin skin($color, $size) {
    @extend %center;
    background: $color;
    height: $size;
}

a {
    @include skin(pink, 10em)
}

b {
    @include skin(blue, 90px)
}

//********************编译输出******************** 
a,
b {
    margin-left: auto;
    margin-right: auto;
    display: block;
}

a {
    background: pink;
    height: 10em;
}

b {
    background: blue;
    height: 90px;
}
```


##四 、SASS编程规范

### 4.1 语法格式  

#### 4.1.1 字符串

虽然 Sass 中的字符串不强制要求使用引号包裹，但是包裹起来，显然具有更好的可读性。此外，还有一些理由也强调了这种包裹的重要性： 

- 如果颜色名不被引号包裹，将会被解析为颜色值，显然这会导致严重问题；
- 大多数的语法高亮机制将会因未被引号包裹的字符串而罢工。

#### 4.1.2 数值

在 Sass 中给变量赋予数值并运算，其中最需要注意的就是运算过程的单位：将一个单位添加给数字的时候，实际上是让该数值乘以1个单位。
    
```scss
$value: 42;
// Yep
$length: $value * 1px;
// Nope
$length: $value + px;
```

要删除一个值的单位，你需要除以相同类型的1单位。

```scss
$length: 42px;
// Yep
$value: $length / 1px;
// Nope
$value: str-slice($length + unquote(‘’), 1, 2);
```

#### 4.1.3  颜色

为了尽可能简单地使用颜色，建议将颜色按照以下顺序排列：

- CSS 颜色关键字;
- HSL 值;
- RGB 值;
- 十六进制。小写并尽可能简写。

当一个颜色被多次调用时，最好用一个有意义的变量名来保存它。

```scss
$sass-pink: #c69;
$main-theme-color: $sass-pink;
```

#### 4.1.4 列表 list 

列表相当于 Sass 的数组。与map不同，列表可以保存任意类型的数值，包括其他列表。

```scss
// Yep
$font-stack: ‘Helvetica’, ‘Arial’, sans-serif;
// Nope
$font-stack:
  ‘Helvetica’,
  ‘Arial’,
  sans-serif;
// Nope
$font-stack: ‘Helvetica’ ‘Arial’ sans-serif;
```

当需要给列表添加一个新列表项时，请遵守其提供的API，不要试图手动给列表添加列表项。

```scss
$shadows: 0 42px 13.37px hotpink;

// Yep
$shadows: append($shadows, $shadow, comma);

// Nope
$shadows: $shadows, $shadow;
```

#### 4.1.5 map 

- 冒号(:)之后添加空格；
- 如果键是字符串（99%都是字符串），则使用括号包裹起来。
- 每一个键值对单独一行；
- 每一个键值对以逗号(,)结尾；
- 为最后一个键值对添加尾部逗号 (,)，方便添加新键值对、删除和重排已有键值对。

```scss
// Yep
$breakpoints: ( 'small': 767px, 'medium': 992px, 'large': 1200px, );
// Nope
$breakpoints: ( small: 767px, medium: 992px, large: 1200px);
```

使用map可以创建map-get函数以提供友好的api功能

```scss
// Z-indexes map, gathering all Z layers of the application

// @access private
// @type Map
// @prop {String} key - Layer’s name
// @prop {Number} value - Z value mapped to the key
$z-indexes: ( 'modal': 5000, 'dropdown': 4000, 'default': 1, 'below': -1);


// Get a z-index value from a layer name

// @access public
// @param {String} $layer - Layer’s name
// @return {Number}
// @require $z-indexes
@function z($layer) {
    @return map-get($z-indexes, $layer);
}
```

#### 4.1.6 混合宏@mixin

如果发现有一组css属性经常出现，则可以使用混合宏来代替。
     
```scss
//示例一

/// Helper to clear inner floats
/// @author Nicolas Gallagher
/// @link http://nicolasgallagher.com/micro-clearfix-hack/ Micro Clearfix
@mixin clearfix {
  &::after {
	content: '';
	display: table;
	clear: both;
  }
}

//示例二

/// Helper to size an element
/// @author Hugo Giraudel
/// @param {Length} $width
/// @param {Length} $height
@mixin size($width, $height: $width) {
  width: $width;
  height: $height;
}
```

@content在sass3.2.0中引入，可以用来解决css3的@media等带来的问题。它可以使@mixin接受一整块样式，接受的样式从@content开始。

```scss
@mixin max-screen($res) {
    @media only screen and ( max-width: $res) {
        @content;
    }
}

@include max-screen(480px) {
    body {
        color: red;
    }
}

//********************编译输出******************** 
body {
    color: red;
}
```

#### 4.1.7 继承

sass中，选择器继承可以让选择器继承另一个选择器的所有样式，并联合声明。使用选择器的继承，要使用关键词@extend，后面紧跟需要继承的选择器。

```scss
h1 {
    border: 4px solid #ff9aa9;
}

.speaker {
    @extend h1;
    border-width: 2px;
}

//********************编译输出********************
h1,
.speaker {
    border: 4px solid #ff9aa9;
}

.speaker {
    border-width: 2px;
}
```

#### 4.1.8  函数

sass定义了很多函数可供使用，当然你也可以自己定义函数，以@fuction开始。

#### 4.1.9 参数列表

对于不定参数，可以使用 … 来表示：

```scss
@mixin shadows($shadows…) {
  // type-of($shadows) == 'arglist'
  // …
}
```

Sass的混合宏和函数声明非常智能，你只需给函数/混合宏一个列表或map，它会自动解析为一系列的参数。
    
```scss
@mixin dummy($a, $b, $c) {
  // …
}

// Yep
@include dummy(true, 42, 'kittens');

// Yep but nope
$params: true, 42, 'kittens';
$value: dummy(nth($params, 1), nth($params, 2), nth($params, 3));

// Yep
$params: true, 42, 'kittens';
@include dummy($params…);

// Yep
$params: (
  'c': 'kittens',
  'a': true,
  'b': 42
);
@include dummy($params…);
```


#### 4.1.10  条件语句

`Sass` 通过 `@if `和 `@else` 指令提供了条件语句。

```scss
// Yep
@if $support-legacy {
  // …
} @else {
  // …
}

// Nope
@if ($support-legacy == true) {
  // …
}
@else {
  // …
}
```

测试一个错误值时，通常使用`not`关键字而不是比较与`false`或`null`等值。

```scss
// Yep
@if not index($list, $item) {
  // …
}

// Nope
@if index($list, $item) == null {
  // …
}
```

当使用条件语句并在一些条件下有内联函数返回不同结果时，始终要确保最外层函数有一个`@return`语句。

```scss
// Yep
@function dummy($condition) {
    @if $condition {
        @return true;
    }
    @return false;
}

// Nope
@function dummy($condition) {
    @if $condition {
        @return true;
    }
    @else {
        @return false;
    }
}
```

#### 4.1.11  循环语句

`@each` 循环绝对是 `Sass`提供的三个循环方式中最常用的。它提供了一个简洁的` API `来迭代`list`或`map`。

```scss
@each $theme in $themes {
  .section-#{$theme} {
	background-color: map-get($colors, $theme);
  }
}
```

当迭代一个`map`时，通常使用`$key`和`$value`作为变量名称来确保一致性。

```scss
@each $key, $value in $map {
  .section-#{$key} {
	background-color: $value;
  }
}
```

### 4.2 命名约定

#### 4.2.1 常量

使用大写加下划线的形式命名常量

```scss
// Yep
$CSS_POSITIONS: top, right, bottom, left, center;
// Nope
$css-positions: top, right, bottom, left, center;
```
#### 4.2.2响应式设计 

断点不应该根据具体的设备来命名，而应使用更通用的名字：

```scss
// Yep
$breakpoints: (
  'medium': (min-width: 800px),
  'large': (min-width: 1000px),
  'huge': (min-width: 1200px),
);

// Nope
$breakpoints: (
  'tablet': (min-width: 800px),
  'computer': (min-width: 1000px),
  'tv': (min-width: 1200px),
);
```

一旦用自己钟意的方式命名完断点，就需要有一种方式在实际的媒体查询中使用它。

```scss
/// Responsive manager.
/// @access public
/// @param {String} $breakpoint - Breakpoint
/// @requires $breakpoints
@mixin respond-to($breakpoint) {
    @if map-has-key($breakpoints, $breakpoint) {
        @media #{inspect(map-get($breakpoints, $breakpoint))} {
            @content;
        }
    }
    @else {
        @error 'No value found for `#{$breakpoint}`. '+'Please make sure it is defined in `$breakpoints` map.';
    }
}
```

### 4.3 命名空间

使用一个独特的前缀标示命名空间，既不会引发命名冲突，又足够简明精练。

```scss
$su-configuration: ( …);
@function su-rainbow($unicorn) {
    // …
}
```

### 4.4 组织架构

```bash
sass/
|
|– base/
|   |– _reset.scss   # Reset/normalize
|   |– _typography.scss  # Typography rules
|   …  # Etc…
|
|– components/
|   |– _buttons.scss # Buttons
|   |– _carousel.scss# Carousel
|   |– _cover.scss   # Cover
|   |– _dropdown.scss# Dropdown
|   …  # Etc…
|
|– layout/
|   |– _navigation.scss  # Navigation
|   |– _grid.scss# Grid system
|   |– _header.scss  # Header
|   |– _footer.scss  # Footer
|   |– _sidebar.scss # Sidebar
|   |– _forms.scss   # Forms
|   …  # Etc…
|
|– pages/
|   |– _home.scss# Home specific styles
|   |– _contact.scss # Contact specific styles
|   …  # Etc…
|
|– themes/
|   |– _theme.scss   # Default theme
|   |– _admin.scss   # Admin theme
|   …  # Etc…
|
|– utils/
|   |– _variables.scss   # Sass Variables
|   |– _functions.scss   # Sass Functions
|   |– _mixins.scss  # Sass Mixins
|   |– _helpers.scss # Class & placeholders helpers
|
|– vendors/
|   |– _bootstrap.scss   # Bootstrap
|   |– _jquery-ui.scss   # jQuery UI
|   …  # Etc…
|
|
|– main.scss # primary Sass file
```

- `base/ `文件夹存放项目中的模板文件。

  在这里，可以找到重置文件、排版规范文件或者一个样式表（我通常命名为 `_base.scss`）——定义一些 HTML 元素公认的标准样式。

- `layout/ `文件夹存放构建网站或者应用程序使用到的布局部分。

  该文件夹存放网站主体（头部、尾部、导航栏、侧边栏…）的样式表、栅格系统甚至是所有表单的 CSS 样式。

- 相对于 `layout/ `的宏观（定义全局线框结构），`components/` 更专注于局部组件。

  该文件夹包含各类具体模块，基本上是所有的独立模块，比如一个滑块、一个加载块、一个部件……由于整个网站或应用程序主要由微型模块构成，`components/` 中往往有大量文件。

- 如果页面有特定的样式，最好将该样式文件放进 pages/ 文件夹并用页面名字。例如，主页通常具有独特的样式，因此可以在 `pages/` 下包含一个` _home.scss` 以实现需求。

- 在大型网站和应用程序中，往往有多种主题。虽有多种方式管理这些主题，但是我个人更喜欢把它们存放在 `themes/` 文件夹中。

- `utils/` 文件夹包含了整个项目中使用到的 Sass 辅助工具

  这里存放着每一个全局变量、函数、混合宏和占位符。

- `vendors/` 文件夹用来存放所有外部库和框架

  （`Normalize, Bootstrap, jQueryUI, FancyCarouselSliderjQueryPowered……`）的` CSS` 文件。

  将这些文件放在同一个文件中是一个很好的说明方式:”嘿，这些不是我的代码，无关我的责任。”

- 最后是 `main.scss`，它的作用是聚合所有的其他文件。

  为了保持可读性，主文件应遵守如下准则：

  - 每个 `@import`引用一个文件；
  - 每个` @import`单独一行；
  - 从相同文件夹中引入的文件之间不用空行；
  - 从不同文件夹中引入的文件之间用空行分隔；
  - 忽略文件扩展名和下划线前缀。


