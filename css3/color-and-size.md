# color and size

[TOC]

## color
当一个网页展示在人们面前的时候，给人第一印象的不是它的内容，也不是它的设计，而是色彩的搭配。因此，颜色对于网页的设计尤为重要。网站颜色的使用好坏，直接影响到网站的生存能力。

颜色值随着计算机的发展不断变得丰富：
216中web安全色：8位
三原色：24位
增加灰度值：32位

web演示使用的是加色混合，即#000000表示没有颜色，是黑色。
都使用十六进制表示方法。
### 安全色

不同的操作系统和浏览器都有自己的调色板，同一幅图在不同系统或浏览器中可能显示的颜色差别很大。这是因为，选择特定的颜色值时，浏览器会使用本身调色板中最接近的颜色。如果浏览器中没有所选的颜色，就会通过抖动或者混合自身的颜色来尝试重新产生改颜色。

为了解决调色板不同的问题，人们挑选了一组在所有浏览器中都类似的颜色。这些颜色使用了一种颜色模型，这个模型中可以使用十六进制 00、33、66、99、CC、FF来表达三原色的每一种。每个原色6种，6 * 6 * 6 = 216种颜色（其中彩色为210种，非彩色6种）。构成了web安全色。

216 种安全色在显示搞定度的渐变效果或显示真彩图像或照片时会略显不足，但是显示会标或者二维平面效果图是却绰绰有余。

### 颜色模式

#### RGB 色彩模式

RGB 色彩模式使光的三原色 red、green、blue 混合产生的。是一种加色混合模型。

#### CMYK 色彩模型

CMYK 是指颜料的三原色 青色、洋红、黄色加上黑色，这四种颜色混合表现出的色彩用绘画和印刷品。是一种减色模型。

#### 索引色彩模型

索引色彩模型已被限定在256种颜色以内的模式，主要用于web网页安全色和制作透明gif图片。
#### 灰度模式

灰度模式无颜色，制作黑白图片时使用。
#### 双色模式

在黑白图片中加入颜色。

#### 位图模式

### opacity 透明度

opacity: alphavalue || inherit;

- alphavalue: 0 ~ 1 之间的任意浮点数。1时不透明，0时完全透明。
- inherit: 继承父元素而的透明度。

透明度是针对真个元素的，跟alpha通道是两个概念。alpha通道只是应用于颜色。

transparent 也用于给颜色设置透明度，相当于alpha通道设置为0。任何指定颜色值的属性中都可以使用 transparent 值。

### CSS3 颜色模式
CSS3 新增了 RGBA、HSL、HSLA颜色模式。

#### RGBA
RGBA 是在 RGB 的基础上增加了alpha通道的值。

表示方法
rgba(r, g, b, a)
a 可以取 0 ~ 1 之间的范围。

#### HSL

HSL是颜色的另一种表示方法。 色调H（Hue）、饱和度S（Saturation）、亮度L（Lightness）三个颜色通道的变化和相互叠加可以得到各式各样的颜色。

hsl(h, s, l);

h: 色调是色调盘的一个角度值，0 ~ 360 的任意整数，大于或小于这个范围，都是对360的取模。60表示黄色，120表示绿色，180表示青色，240表示蓝色，300表示洋红。
s: 饱和度是颜色的深浅程度和鲜艳程度，可以是0 ~ 100%之间的任意值，
l: 亮度也是 0 ~ 100% 之间的任意值。0 表示最暗的黑色，100%表示最亮的白色。

#### HSLA

HSLA 是在 HSL 的基础上增加了一个透明度 A 参数。改参数和RGBA的含义和取值一样。
hsla(h, s, l, a);

## 配色

在设计一个网站的时候，先选择一个主色调，然后在同一个色系进行选色和配色。这样，再能保证整个网页色彩丰富，又不会让网页显得花哨。


## 颜色值缩写
关于颜色的css样式也是可以缩写的，当你设置的颜色是16进制的色彩值时，如果每两位的值相同，可以缩写一半。

例子1：

p{color:#000000;}
可以缩写为：

p{color: #000;}
例子2：

p{color: #336699;}
可以缩写为：

p{color: #369;}


## 长度值
长度单位总结一下，目前比较常用到px（像素）、em、% 百分比，要注意其实这三种单位都是相对单位。

1、像素

像素为什么是相对单位呢？因为像素指的是显示器上的小点（CSS规范中假设“90像素=1英寸”）。实际情况是浏览器会使用显示器的实际像素值有关，在目前大多数的设计者都倾向于使用像素（px）作为单位。

2、em

就是本元素给定字体的 font-size 值，如果元素的 font-size 为 14px ，那么 1em = 14px；如果 font-size 为 18px，那么 1em = 18px。如下代码：

p{font-size:12px;text-indent:2em;}
上面代码就是可以实现段落首行缩进 24px（也就是两个字体大小的距离）。

下面注意一个特殊情况：

但当给 font-size 设置单位为 em 时，此时计算的标准以 p 的父元素的 font-size 为基础。如下代码：

html:

<p>以这个<span>例子</span>为例。</p>
css:

p{font-size:14px}
span{font-size:0.8em;}
结果 span 中的字体“例子”字体大小就为 11.2px（14 * 0.8 = 11.2px）。

3、百分比

p{font-size:12px;line-height:130%}
设置行高（行间距）为字体的130%（12 * 1.3 = 15.6px）。