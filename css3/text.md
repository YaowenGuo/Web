# text

[TOC]

## font 字体属性

### font-family 字体

### font-style 字体样式

- normal: 默认值
- italic: 斜体
- oblique: 倾斜

### font-weitht 字体粗细

除了关键字外，还可以设置数字。数字越大表示越粗。常用的是100 ~ 900。
- lightr: 细体
- normal: 默认值
- bord: 粗体
- border: 特粗体


### font-size-adjust

定义是否强制对文本使用同一尺寸。

### font-stretch 横向拉伸

定义是否横向拉伸变形字体

### font-variant 字体大小写

- normal: 默认值
- small-caps: 小写型的大写字母字体

## text 文本

### word-spacing 词间距

- mormal: 默认值。
- 像素，可以是负数

### letter-spacing 字符间距

- mormal: 默认值。
- 像素，可以是负数

### vertical-align 垂直对齐方式

- baseline: 默认值
- sub: 上标对齐
- super: 下标对齐
- bottom: 行框底端对齐
- text-bottom: 行内文本底端对齐
- top: 顶端对齐
- medium: 居中对齐
- 百分数，数字:

### text-decoration 文本的修饰线

- none: 无，默认
- underline: 下换线
- overline: 上划线
- line-through: 删除线
- blink: 闪烁线

取消 a 标签的下划线

```css
a{ text-decoration:none}
```

### text-indent 文本首行缩进

长度单位或百分比

### text-again 文本水平对齐方式

- left:
- center:
- right:
- jutisfy: 两端对齐


### line-height 行高

- normal:
- 长度、百分比、数字:

### text-transform 文本大小写

- mormal: 原样，默认值。
- uppercase: 大写
- lowercase: 小写
- capicalize: 首字母大写。

### text-shadow 文本阴影效果

text-shadow: none | <offset> [blur-redius] [color] [, <offset> [blur-redius] [color] ...]

- color: 阴影色，可以放在最前面也可以放在最后面，是一个可选参数。默认为文本上色。
- x-offset: 水平偏移
- x-offset: 垂直偏移
- blur-redius: 模糊半径，可选参数。

 可以用逗号分隔多个阴影，来为文本设置多个阴影。

### white-space 文字间和文本间的空白符间距

- normal:
- nowrap: 空白符合并，换行符忽略
- pre: 合并空白符、换行符保留
- pre-wrap: 空白符、换行符保留
- pre-line: 空白符合并，换行符保留

### direcrion 文本流入的方向

- ltr:
- rtl:
- inherit:

### text-overflow 文本溢出

- clip: 裁切
- ellipsis: 省略号

仅决定文本溢出时是否显示省略号，并不具备定义样式的功能。要想文本溢出时显示省略号，还需要在一行显示（text-sapce:no-wrap）和溢出文本隐藏（overflow:hidden），并且需要定义容器的宽度。

## word-wrap 换行方式

- break-word: 单词间换行
- break-all: 任意字符间换行
- keep-all: 只能在半角空格或连字符后换行。

## 字体缩写
网页中的字体css样式代码也有他自己的缩写方式，下面是给网页设置字体的代码：

body{
    font-style:italic;
    font-variant:small-caps;
    font-weight:bold;
    font-size:12px;
    line-height:1.5em;
    font-family:"宋体",sans-serif;
}
这么多行的代码其实可以缩写为一句：

body{
    font:italic  small-caps  bold  12px/1.5em  "宋体",sans-serif;
}
注意：

1、使用这一简写方式你至少要指定 font-size 和 font-family 属性，其他的属性(如 font-weight、font-style、font-variant、line-height)如未指定将自动使用默认值。

2、在缩写时 font-size 与 line-height 中间要加入“/”斜扛。

一般情况下因为对于中文网站，英文还是比较少的，所以下面缩写代码比较常用：

body{
    font:12px/1.5em  "宋体",sans-serif;
}
只是有字号、行间距、中文字体、英文字体设置。


CSS显示指定行数文本

1.单行文本溢出用省略号显示：

```css
overflow:hidden;
text-overflow:ellipsis;
white-space:nowrap;
```

2.多行文本溢出用省略号显示：

```css
display: -webkit-box;
-webkit-box-orient: vertical;
-webkit-line-clamp: 3;
overflow: hidden;
```