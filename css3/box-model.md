# Box model

[TOC]

css 将每一个元素看做是一个盒子，以此来解释各种属性，这种方式被称为盒模型。css 主要有以下几种盒模型：inline、inline-bolck、block、table、absolute position、float。每个盒模型是有以下几个属性组合所决定的：display、position、float、width、height、margin、padding和border等。不同的盒模型会产生不同的布局。

- Z-轴层叠：padding, content, background-img, background-color;
- 平面：border, margin, padding平面上的关系，并不能过程Z-轴的层叠。

![盒模型](./images/box-model/standard-box-model.jpg)


> 外盒尺寸计算（元素空间尺寸）

element 空间高度 = 内容高度 + 内距 + 边框 + 外距
element 空间宽度 = 内容宽度 + 内距 + 边框 + 外距

> 内核储存计算（元素大小）

element 高度 = 内容高度 + 内距 + 边框
element 宽度 = 内容宽度 + 内距 + 边框

***【待测试】但是对于form中部分元素还基于ID的传统的盒模型，例如input中的submit、reset、button、select等元素***

#### 块级元素都具备盒子模型的特征

##### 边框（一）
盒子模型的边框就是围绕着内容及补白的线，这条线你可以设置它的粗细、样式和颜色(边框三个属性)。
```
div{
    border:2px  solid  red;
}
div{
    border-width:2px;
    border-style:solid;
    border-color:red;
}
```

注意：

1、border-style（边框样式）常见样式有：

dashed（虚线）| dotted（点线）| solid（实线）。


2、border-color（边框颜色）中的颜色可设置为十六进制颜色，如:

border-color:#888;//前面的井号不要忘掉。

3、border-width（边框宽度）中的宽度也可以设置为：

thin | medium | thick（但不是很常用），最常还是用象素（px）。

div{border-bottom:1px solid red;}


##### 填充pandding 边界margin
元素内容与边框之间是可以设置距离的，称之为“填充”。填充也可分为上、右、下、左(顺时针)。如下代码：

div{padding:20px 10px 15px 30px;}

如果上、右、下、左的填充都为10px;可以这么写
div{padding:10px;}

如果上下填充一样为10px，左右一样为20px，可以这么写：
div{padding:10px 20px;}

## css3 盒模型属性

标准的浏览器中，盒模型的高度和宽度仅仅包含了内容的宽度，出去了边框和内边距两个区域，这位Web设计处理效果增加了很多麻烦。为了解决这个问题，CSS3增添了一个盒模型属性box-zizing，能够实现定义盒模型尺寸解析方式。语法如下：
```
box-sizing: content-box | border-box | inherit
```

- content-box: 默认值，让元素维持W3C的标准盒模型。
- border-box: 让元素模型的解析改用IE传统的盒模型，元素的宽度=内边距 + 内容宽度 + 边框；高度=内边距 + 内容高度 + 边框。
- inherit: 元素继承父元素的盒模型模式。

## overflow css3内容溢出属性
在css中每一个元素都视为一个盒子，这个盒子就是一个容器。容器如果指定了固定的大小，内容过多时就会容纳不下。此时可以使用overflow属性来指定该如何显示何种容纳不下的内容。CSS3增加overflow-x和overflow-y来单独指定某个方向。

支持的属性值：

- visible: 默认值，不剪切容器中的任何内容，不添加滚动，元素将被剪切成包含对象大小的窗口对象。
- hidden: 内容溢出时，所有内容都隐藏，并且不显示滚动条。
- scroll: 不管内容有没有溢出，overflow-x都会显示横向的滚动条，而overflow-y会显示纵向的滚动条。
- auto: 在超出设定的大小时剪切内容，超出部分被隐藏，并显示滚动条。
- （不支持了？）no-display: 当内容溢出时，不显示整个元素，此时类似于元素添加了display:none。
- （不支持了？）no-content: 内容溢出时，不显示内容，此时类似于添加了sivibility：hidden声明。
- inherit: 继承父元素
- initial:
- unset:
- overlay:

## resize 自由缩放属性

***必须和overflow 同时使用*** 允许用户通古拖动的方式修改元素的尺寸来改变元素大小

none: 不能拖动元素而修改元素大小。
both: 可以通过拖动修改元素的宽度和高度
horizontial: 仅能够修改元素的宽度
vertical: 仅能够修改元素的高度
inherit: 继承父元素的属性值。

textarea 的默认 resize 属性设置为 both，可以通过修改resize属性值修改textarea的行为。

## outline 外轮廓属性

主要用户设置元素外的显示效果。外轮廓线不占用网页布局空间，不一定是矩形，外轮廓是一种动态样式，只有元素获得焦点或者被激活时呈现。

outline: [outline-color]||[outline-style]||[outline-width]||[outline-offset]|| inherit

- outline-offset: 定义轮廓边框的偏移位置的数值，此值可以取负值。当值取整数时，表示轮廓向外偏离多少像素；当值取负数时，表示轮廓向内偏移多少像素。

其他值同border 属性一致。

> 与border 对比

- 不会影响元素的大小，因此不会影响文档流，也不会破坏网页布局。

- border 可以设置个边框不一样，也可以单边设置。但是outline各边只能统一设置，始终是闭合的。
- outline 设置的外轮廓线可能是非矩形的，如果元素是多行，外轮廓线就至少是能够包含该元素所有框的外轮廓。可border不一样，它将使用一个边框包括整个元素。
- border只能向外扩展。而outline既可以向内，也可以向外扩展。

## 盒模型代码简写
还记得在讲盒模型时外边距(margin)、内边距(padding)和边框(border)设置上下左右四个方向的边距是按照顺时针方向设置的：上右下左。具体应用在margin和padding的例子如下：

margin:10px 15px 12px 14px;/*上设置为10px、右设置为15px、下设置为12px、左设置为14px*/
通常有下面三种缩写方法:

1、如果top、right、bottom、left的值相同，如下面代码：

margin:10px 10px 10px 10px;
可缩写为：

margin:10px;
2、如果top和bottom值相同、left和 right的值相同，如下面代码：

margin:10px 20px 10px 20px;
可缩写为：

margin:10px 20px;
3、如果left和right的值相同，如下面代码：

margin:10px 20px 30px 20px;
可缩写为：

margin:10px 20px 30px;
注意：padding、border的缩写方法和margin是一致的。
