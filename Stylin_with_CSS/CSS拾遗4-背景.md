![](leanote://file/getImage?fileId=59f69541ab64410aff000c90)

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

![](leanote://file/getImage?fileId=59f69541ab64410aff000c91)

，CSS3 还规定另外两个值（但尚未得到浏览器支持），以控制背景图片重复确切的次数，即所有图片都是完整的，不会出现半张图片的现象。

- background-repeat:round：为确保图片不被剪切，通过调整图片大小来适应背景区域。
- background-repeat:space，为确保图片不被剪切，通过在图片间添加空白来适应背景区域。