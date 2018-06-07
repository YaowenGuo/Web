# media type

W3C 共定义了 10 种媒体类型

- all: 所有设置
- braille: 盲人用点字法触觉回馈设备
- embossed: 盲文打印机
- handheld: 便携设备
- print: 打印设备，或打印模式
- projection: 各种投影设备
- screen: 电脑显示器
- speech: 语音或音频合成器
- tv: 电视机类型设备
- tty: 使用固定密度字母山歌的媒介，比如电传打印机和终端。

## 常用的媒体类型引用方法

link 标签, xml 方式, @import, @media

### link 标签

link 方法引入媒体类型其实是在 <link> 标签引用样式的时候，通过 link 标签中的 media 属性来指定不同的媒体类型。这种方式引入媒体类型时常跟着引用样式文件走，如下所示。

```
<link rel="stylesheet" type="test/css" href='style.css' media='screen'/>
<link rel="stylesheet" type="test/css" href='print.css' media='print'/>
```

### xml 方式

xml 引用媒体类型和 link 引入媒体类型及其相似，也是通过 media 属性来指定。

```
<?xml-stylesheet rel="stylesheet" type="test/css" href='screen.css' media='screen'/>
```

### @import

@ import 是在 css 文件中导入另一个 CSS 文件，同样也可以用来引用媒体类型。@import 引入的媒体类型主要有两种方式，一种是在样式文件中通过 @import 调用另一个样式文件。另一个是在 html 标签中的 <style></style> 标签中引入。

```
@import url(screen.css) screen;
@import url(style.css) all;
```

### @media

@media 称为媒体查询。@media 引入的地方和 @import 一样，也有一样的两种类型。引入的方式为
```
@media screen {
    /* 样式 */
}
```

***以上各种方式在使用中各有利弊，在实际使用建议使用 `link` 标签和 `@media` 的方式。***


## 媒体查询（Media Query）

在之前想要根据屏幕类型或宽度引入一个样式，可以这样写
```
<link rel="stylesheet" type="test/css" href='small.css' media='screen and (max-width:600px)'/>
```
在 CSS3 中，可以通过如下的样式写在 CSS 文件中

```
@media screen and (mas-width:600px) {
    /*新的 CSS 选择器和样式*/
}
```

虽然 媒体查询和 CSS 的属性集合很相似，还是有差别的：

- Medai Query 只接受单个的逻辑表达式作为其值，或者没有值。
- CSS 属性集合用于声明如何表现页面的信息； 而 Media Query 是一个用于判断输出设备是否满足某种条件的表达式。
- Media Query 中的大部分接受 min/max 前缀，用来表达逻辑关系，表示应用于大于等于或小于等于某个值的情况。
- CSS 属性要求必须写属性值，Media Query 可以没有值，因为表达式返回的之后真或假两种状态。


### 常用的 Media Query 设备特征

W3C 共列出13中 CSS3 中常用的特征。

| 属性            | 值             |    Min/Max     |    描述        |
| :------------- | :------------- | :------------- | :------------- |
| color          | 整数            |  Yes           | 每种亚颜色的字节数|
| color-index    | 整数            |  Yes           | 色彩表中的色彩数 |
| device-aspect-ratio | 整数/整数   |  Yes           | 宽高比例       |
| device-height  | Lenght         |  Yes           | 设备屏幕的输出高度|
| device-width   | Lenght         |  Yes           | 设备屏幕的输出宽度|
| grid           | 整数            |  No            | 是否基于的那个的设备|
| height         | Lenght         |  Yes           | 渲染界面的高度   |
| monochrome     | 整数            |  Yes           | 单色帧缓冲器中每像素字节|
| relolution     | 分辨率(dpi/dpcm)|  Yes           | 分辨率          |
| scan           | Progressive interlaced |  No    | Tv 媒体类型的扫描方式|
| width          | Length         |  Yes           | 渲染界面的宽度    |
| orientation    | Portrait/landscape |  No        | 横屏或竖屏       |


### 使用方式

```
@media 媒体类型 and(媒体特征) {
    应用的样式
}
```

媒体特征使用 `媒体特征: 媒体特征值`。 如

```
max-width: 480px
```
则此媒体查询中的样式将应用在显示宽度在 480px 以下的网页中，样式生效。

### 多个媒体的使用

```
@media screen and (min-width:600px) and (max-width:900px) {

}
```

### not 排除媒体类型

关键词 not 用于排除某种特定的媒体类型，如
```
@media not print and （max-width: 1200px） {

}
```

### only


## 响应是布局

将三种已有的开发技术（弹性网格布局、弹性图片、媒体和媒体查询）整合起来，将其命名为 Reponsive Web Design. RWD 能够让网页在不同的设备中展现不同的设计风格。

### 响应式布局的特点

响应式网页设计不但要考虑其元素布局的秩序，还要做到“有求必应”。因此需要满足三个条件，响应式布局之父 Ethan Marcotte 是这样描述着三个条件的。
- 网站必须建立灵活的网格基础
- 引用到的网站的图片必须是可伸缩的
- 不同的显示风格，需要再 Media Query 上设置不同的样式。

### 术语

> 流体网格

流体网格是一种简单的网格系统，这种网格设计参考了流体设计中的网格系统，将每个网格格子使用百分比单位来控制网格大小。这种网格系统最大的好吃是让网格大小随时根据屏幕尺寸大小做出相应的比例缩放。

> 弹性图片

是指不给图片社会固定的尺寸，而是滚局流体网格进行缩放，用于适应各种网格的尺寸。而实现方法比较简单

```
img {width: 100%;}
```

给不同的断点提供不同的图片能够达到比较好的显示效果，然而 Media Query 并不能改变 src 属性的值。解决办法：
- 使用 background-image 给元素添加背景图片
- 显示/隐藏父元素，给父元素使用不同的图片，然后通过媒体查询控制这些父元素的隐藏或显示（不建议）

> 主要断点

是指显示设备最多个几个设备宽度临界点。媒体查询通常是对这些临界点判断应用样式的。常用的临界点有：
320px、480px、640px、768px.

在实际中可以根据需要增加次要断点，但是要注意，随着断点的增加，维护成本也在增加，所以要可以控制断点数量。


### 响应式布局技巧

要想设计好响应式布局，首先要做的就是让页面布局尽量简单，实现一个简单的布局有一些小的技巧。

- 尽量少使用无关紧要的 div
- 不要使用内联元素
- 尽量少使用 JS 或 FLASH
- 丢弃没用的绝对定位和浮动样式
- 摒弃任何冗余结构和不适用100%设置

有舍才有得，哪些东西能帮助 Responsive 确定更好的布局呢？

- 使用 HTML5 Doctype 和相关指南
- 重置好样式（reset。css）
- 一个简单的有语义的核心布局
- 给重要的网页元素使用简单的技巧，比如导航菜单之类元素。
- 主要显示区域不要过分依赖现代技巧来实现比如说 CSS3 特效或者 JS 脚本

### mete 标签

当在移动设备测试响应布局的时候，会发现媒体查询都不会生效——页面仍展示为普通的样式，即一个全局缩小后的页面。这是因为许多只能手机都是用了一个比世界屏幕尺寸大很多的虚拟可视区域，主要目的就是让页面在只能手机端阅读是不会因为实际可视区域而变形。为了能够让浏览器以实际的可视区域显示样式。需要天界一个特殊的 meta 标签。该标签用于告诉浏览器，如何优化显示效果，并且可以自定义界面可视区域的尺寸和缩放界别

```
<meta name="viewport" content="" />
```

content 可以使用的值
- width: 可视区域的宽度，其值可以是一个具体数字或关键词 device-width 表示实际屏幕宽度
- height: 可视区域的高度，其值可以是一个具体数字或关键词 device-height 表示实际屏幕高度
- initial-scale: 页面首次被显示时可视区域的缩放级别，取值为1.0是将是页面按实际尺寸显示，无任何缩放。
- minimun-scale: 可视区域的最小缩放级别，表示用户可以将页面缩小的程度，取值为 1.0 时将禁止用户缩小至实际尺寸以下。
- maximun-scale: 可视区域的最大缩放级别，表示用户可以将页面放大的程度，取值为 1.0 时将禁止用户放大至实际尺寸以上。
- user-scalable: 指定用户是否可以对页面进行缩放，yes:允许；no: 禁止缩放。

要想在移动设备中应用媒体查询，需要设置meta为
```
<meta name="viewport" content="width=divice-width, initial-scale=1.0"/>
```
