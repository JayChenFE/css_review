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
/只在屏幕宽度不大于568 像素时应用/

@media screen and (max-width:568px) {
	.column {float:none; width:96%; margin:0 auto;}
}

```

如果页面是通过屏幕显示，而且该屏幕宽度不超过568 像素，那么CSS 就会取消带`.column ` 类的元素的浮动，让布局区块上下堆叠，且让该元素宽度为屏幕的96%，同时在屏幕上居中

iPhone 4 的屏幕分辨率为320×480，而iPhone 5 的屏幕分辨率则为320×568(**像素是翻倍使用的——物理像素在两个方**
**向上都是这里值的两倍**)