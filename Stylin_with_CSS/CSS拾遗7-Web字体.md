# Web 字体

设定Web 字体的方式有以下三种。

- 使用`Google Web Fonts `或`Adobe` 的`Typekit` 等公共字体库。 
- 使用事先打好包的`@font-face `包。 
- 使用`Font Squirrel `用你自己的字体生成`@font-face` 包。 

## 公共字体库

打开http://www.google.com/webfonts

##  打包的`@font-face` 包

以这种方式提供的字体，会在使用该字体的页面第一次加载时被浏览器下载并缓存起来，以后就不用下载了

`Font Squirrel`（http://www.fontsquirrel.com） 

`Font Squirrel` 为`Ubuntu Titling Bold `字体生成的`@font-face`  代码

```css
@font-face {
    /*这就是将来在字体栈中引用的字体族的名字*/
    font-family: 'UbuntuTitlingBold';
    src: url('UbuntuTitling-Bold-webfont.eot');
    src: url('UbuntuTitling-Bold-webfont.eot?#iefix') format('embedded-opentype'),
    url('UbuntuTitling-Bold-webfont.woff') format('woff'),
    url('UbuntuTitling-Bold-webfont.ttf') format('truetype'),
    url('UbuntuTitling-Bold-webfont. svg#UbuntuTitlingBold') format('svg');
    font-weight: normal;
    font-style: normal;
}
```

## 生成`@font-face` 包

只要你获得了把该字体转换为Web 字体使用的授权（请查看许可协议或联系字体设计商），就可以使用Font Squirrel 的转换
程序（http://www.fontsquirrel.com/fontface/generator）把它转换成@font-face 字体包

Tim Brown 的博客文章“How to use@font-face”：http://nicewebtype.com/notes/2009/10/30/how-to-use-css-font-face/。

关于多种字体格式的@font-face 规则如何写，以及如何保证Internet Explorer 取得必要的.eot 格式的字体， 可以参考Fontspring 博客的文章：http://www.fontspring.com/blog/fixing-ie9-font-face-problems
