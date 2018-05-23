# Box model

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

## css3 盒模型属性

标准的浏览器中，盒模型的高度和宽度仅仅包含了内容的宽度，出去了边框和内边距两个区域，这位Web设计处理效果增加了很多麻烦。为了解决这个问题，CSS3增添了一个盒模型属性box-zizing，能够实现定义盒模型尺寸解析方式。语法如下：
```
box-sizing: content-box | border-box | inherit
```

- content-box: 默认值，让元素维持W3C的标准盒模型。
- border-box: 让元素模型的解析改用IE传统的盒模型，元素的宽度=内边距 + 内容宽度 + 边框；高度=内边距 + 内容高度 + 边框。
- inherit: 元素继承父元素的盒模型模式。

## overflow css3内容溢出属性
