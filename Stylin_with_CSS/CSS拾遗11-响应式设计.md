# 响应式设计的要素

- 媒体查询:根据浏览器的特性，一般是屏幕或浏览器容器宽度提供CSS 规则
- 流式布局：使用`em`  或百分比等相对单位设定页面总体宽度，让布局能够随屏幕大小而缩放
- 弹性图片：使用相对单位确保图片再大也不会超过其容器。

最早是由`Ethan Marcotte `提出来的，发表在2010 年5 月份的`A List Apart` 杂志上，地址是：http://www.alistapart.com/articles/responsive-web-design

# 媒体查询

下面这个网页列出了针对iOS、安卓和Windows 设备的所有媒体查询：http://pugetworks.com/blog/2011/04/css-media-queries-for-targetingdifferent-mobile-devices/

媒体查询可以用两种方式来写：

- `@media` 规则
- `<link>`标签的`media` 属性

## `@media规则`

例1:

```css
@media print {
	nav {display:none;}
}
```

这条规则声明：如果当前页面要打印，那么就不显示`nav `元素。

> 可以把CSS 规则嵌套在媒体查询里，但媒体查询本身却不能互相嵌套

例2:

```css
/*只在屏幕宽度不大于568 像素时应用*/

@media screen and (max-width:568px) {
	.column {float:none; width:96%; margin:0 auto;}
}

```

如果页面是通过屏幕显示，而且该屏幕宽度不超过568 像素，那么CSS 就会取消带`.column ` 类的元素的浮动，让布局区块上下堆叠，且让该元素宽度为屏幕的96%，同时在屏幕上居中

iPhone 4 的屏幕分辨率为320×480，而iPhone 5 的屏幕分辨率则为320×568(**像素是翻倍使用的——物理像素在两个方**
**向上都是这里值的两倍**)

把`max-width`  设定为较大的iPhone 5 屏幕的最大宽度，可以保证布局各栏在所有iPhone 中都不再浮动，而是上下堆叠

**作者写这篇文章时最大屏幕的iphone为iphone5**

相应设备必须是一块最大屏幕宽度不超过568 像素的屏幕（比如浏览器或智能手机）。因此，这条规则就不会应用给1024×768 像素的iPad。

>想知道怎么在苹果视网膜（retina）屏和其他高分辨率屏上以恰当的分辨率显示图片？
>
>可以参考这篇文章：http://coding.smashingmagazine.com/2012/08/20/towards-retina-web/

## 媒体查询的常见参数

- 媒体类型

  - all：匹配所有设备
  - handled：匹配手持设备（小屏幕、单色、带宽有限）
  - print：匹配分页媒体或打印预览模式下的屏幕
  - screen：匹配彩色计算机屏幕
  - 其他媒体类型
    - braille（盲文点字触觉反馈设备）
    - embossed（盲文分页打印机）
    - projection（投影仪）
    - speech（语音合成器）
    - tty（电话机屏幕等固定宽度字符栅格设备）
    - tv（电视机）

  要想详细了解这些媒体类型，请参考CSS 2.1 标准：http://www.w3.org/TR/CSS2/media.html

  > 任意时刻浏览器窗口中只能使用一种媒体类型。媒体类型从IE6 开始就得到支持

- 媒体特性

  媒体特性也就是媒体某一方面的特征，一般带有`min-`或`max-`前缀。常用的媒体特性如下:

  - `min-device-width` 和`max-device-width`：匹配设备屏幕的尺寸； 
  - `min-width` 和`max-width` ：匹配视口的宽度，例如浏览器窗口宽度；
  - `orientation`（值为`portrait `和`landscape` ）：匹配设备是横屏还是竖屏。

  ​

  要了解所有媒体特性，请参考CSS3 标准：http://www.w3.org/TR/css3-mediaqueries/media1

  使用逻辑运算符and、not、or 及关键字all、only 组合媒体类型和媒体特性

  参考这里：
  https://developer.mozilla.org/en-US/docs/CSS/Media_queries#Operator_precedence

  ​

  关于媒体查询的扫盲文章:

  http://www.javascriptkit.com/dhtmltutors/cssmediaqueries.shtml。

  ​

  至于要在IE8 及以下版本的IE 浏览器中使用媒体查询，可以使用腻子脚本Respond.js

## `<link>`标签的`media` 属性

```css
<link type="text/css" media="print" href="css/print_styles.css" />
<link type="text/css" media="screen and (max-width:568px)"
href="css/iphone_styles.css" />
```

