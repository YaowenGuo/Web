# background

[TOC]

背景包含5个属性： color、image、repeat、attachment、position。

这些属性可以写成缩写形式。

`background: <background-color> [, <background-image>] [, <background-position>] [, <background-size>] [, <background-repeat>] [, <background-attachment>] [, <background-clip>] [,<background-position>]`

可以使用多个以逗号分隔 url 添加多个背景， 但是背景颜色只能有一个。背景图按照先后顺序，从上往下堆叠。

## background-color 颜色

background-color: transparent || <color>;

默认值为 transparent，即不设置任何颜色。颜色可以使用 CSS3 支持的任何格式。

## background-image 图片

background-image: none || url("<img_url>");

相对地址或绝对地址。

## background-repeat 展示方式

background-repeat: repeat || repeat-x || repeat-y || no-repeat;

repeat 是指，在显示区域超图片的平铺方式，即当显示区域超过图片的边缘时，图片重复排列。就像地板的铺放。
默认是两个方向都铺放。

## background-attachment 固定还是滚动

background-attachment: scroll || fixed;

用于设定背景图是否随着页面的其余部分滚动，默认为滚动的。

设置为 fixed 时，一般运用在 html 或 body 标签上，使用在其它标签上不能达到固定效果。

## background-position 位置

background-position: <percentage> || <length> || [left | center | right] [, top | center | bottom];

可以设置一个或两个值，用于表示图片显示的位置。使用数字值时，可以是像素或百分比。
也可以使用预定义的值。

## background-origin 绘制图片的起点

主要用来决定 background-position 属性的参考原点，即决定背景图片的定位的起点.

background-origin: padding-box || border-box || content-box;

- padding-box: background-position 起始位置从 padding的外边缘（padding和border的交界处）开始显示图片。
- border-box: background-position 起始位置为border的外边缘。
- content-box: background-position 起始位置为content的外边缘。

background-attachment 设置为 fixed 时，该属性将不起作用。

## background-clip 裁切显示范围

指定背景图片的裁切区域。

background-clip: padding-box || border-box || content-box;



## background-size 图片尺寸大小

可以指定背景图片的大小

background-size: auto || <length>{1, 2} || <perentage>{1, 2} || cover || content;

- auto: 默认值，保持背景图的原始大小。
- length: 像素指定图片的大小
- percentage: 此百分比是相对于元素的大小计算的。
- cover: 图片以较短的边放大填充整个容器
- contain: 保持图片完整性，以长边缩放整个图片填充整个背景。

## background-break 内联元素的北京图平铺时的循环方式

支持的浏览器较少

background-break: bounding-box || each-box || continuous;

- bounding-box: 背景图像在整个内联元素中进行平铺。
- each-box: 整个行内进行平铺
- continuous: 下一行的背景接着上一行中的图像继续平铺。
