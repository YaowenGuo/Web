# gradient

渐变是两种或多种颜色平滑过渡。

色标：在创建渐变的过程中，可以指定多种之间颜色值，这个值称为色标。每个色标包含一个颜色和一个位置，浏览器从每个色标的颜色淡到下一个，以创建平缓的渐变。

渐变可以应用到任何使用背景图片的地方。在CSS样式中，渐变相当与背景图片，在理论上可在任何使用 url() 值的地方采用，比如常见的 background-image、list-style-type 以及前面介绍的 CSS3 图像边框 border-image。

使用方式
background: linear-gradient(...);

[TOC]

## 线性渐变

线性渐变是指，颜色沿着一条指定的轴向线性过渡。浏览器会绘制与渐变轴垂直的颜色来填充整个容器。

linear-gradient([[<angle> | to <side-or-corder>],]?<color-stop>[,color-stop]+)

- angle: 通过家督来确定渐变方向。0度表示渐变方向从下向上，90度表示渐变方向从左向右。如果取值为下值，其角度按顺时针防线旋转。
- 关键词: 通过角度确定渐变的方向。比如，to top、to right、to bottom、to left、to top left、to top right。
第二个参数和第三个参数表示颜色的起始色和结束色。大家可以从中插入更多的颜色值。

## 径向渐变

radial-gradient([[shape] || [size] [at <position>]?, | at <position>, ]?<color-step> [, <color-step>]+)

- shape: 用来定义径向渐变的形状
    - circle: 如果<size>和<length>带下相等，径向渐变是一个圆形。
    - ellipse: 如果<size>和<length>不相等，径向渐变是一个椭圆形。
- size: 用来确定径向渐变的结束形状大小。如果省略，默认值是 farthest-corner。
    - closest-side: 指定径向渐变的半径长度从圆心到离圆形最近的边。
    - coloset-corner: 指定径向渐变的半径长度从圆心到离圆形最近的角。
    - farthest-size: 指定径向渐变的半径长度从圆心到离圆形最远的边。
    - farthest-corner: 指定径向渐变的半径长度从圆心到离圆形最远的角。
如果 shape 设置为 circle 或者省略，size 肯能显式设置为 lenght。表示用长度值指定径向渐变的横向或纵向长度，并根据横向和纵向的之间来确定径向渐变的形状决定是圆或者是椭圆，不能为负值。

如果 shape 设置为 ellipse 或者省略，size 可以设置为 lenght|parcentage。主要用来设置椭圆的大小。带一个值代表椭圆的水平半径，第二个值代表垂直半径。使用 percentage 定义值是相对于镜像渐变容器的尺寸，不能为负值。

- position: 径向渐变圆心的位置。类似于 background-position 属性。
    - <lenght>: 用长度指定圆心的坐标，可以为负值。
    - <percentage>: 用百分比指定圆心的坐标，可以为负值。
    - left: 设置左边为径向渐变圆心的横坐标值
    - center: 这是中间为圆心的横坐标或纵坐标
    - right: 设置右边为圆心的横坐标
    - top: 设置上边为圆心的纵坐标
    - bottom: 设置下边为圆心的纵坐标。
- color-step: 设置色标颜色。

background-image: redical-gradient(hsla(120, 70%, 60%, .9), hsla(360, 60%, 60%, .9));

> 椭圆渐变

background-image: redical-gradient(ellipsse, hsla(120, 70%, 60%, .9), hsla(360, 60%, 60%, .9));

> 指定圆心 (200px, 150px) 半径 50px，150px

background-image: redical-gradient(50px 150px at 200px 150px, hsla(120, 70%, 60%, .9), hsla(360, 60%, 60%, .9));

> 使用百分数指定圆心和半经

background-image: redical-gradient(50% 80% at 50% 50%, hsla(120, 70%, 60%, .9), hsla(360, 60%, 60%, .9));

> 使用关键词定位

background-image: redical-gradient(50% 80% at center, hsla(120, 70%, 60%, .9), hsla(360, 60%, 60%, .9));

background-image: redical-gradient(50% 80% at left top , hsla(120, 70%, 60%, .9), hsla(360, 60%, 60%, .9));

> 通过关键词设置大小

background-image: redical-gradient(colsient-size circle at left top , hsla(120, 70%, 60%, .9), hsla(360, 60%, 60%, .9));

> 多色渐变

background-image: redical-gradient(colsient-size circle at left top , red, green, blue);

> 设置每个颜色位置

background-image: redical-gradient(colsient-size circle at left top , red 20%, green 50%, blue 80%);

### 重复渐变

想要使用重复渐变，只需要使用 repeating-linear-gradient函数代替线性渐变 linear-gradient， 使用 repeating-redical-gradient 代替 redical-gradient。
