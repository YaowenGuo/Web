#### 标签分类

元素分类
在讲解CSS布局之前，我们需要提前知道一些知识，在CSS中，html中的标签元素大体被分为三种不同的类型：块状元素、内联元素(又叫行内元素)和内联块状元素。

常用的块状元素有：
```html
<div>、<p>、<h1>...<h6>、<ol>、<ul>、<dl>、<li>、<table>、<address>、<blockquote> 、<form>
```
常用的内联元素有：
```html
<a>、<span>、<br>、<i>、<em>、<strong>、<label>、<q>、<var>、<cite>、<code>
```
常用的内联块状元素有：
```html
<img>、<input>
```


#### 块级元素
*** 块级元素都具备盒子模型的特征。***

块级元素特点：

1. 每个块级元素都从新的一行开始，并且其后的元素也另起一行。（真霸道，一个块级元素独占一行）
2. 元素的高度、宽度、行高以及顶和底边距都可设置。
3. 元素宽度在不设置的情况下，是它本身父容器的100%（和父元素的宽度一致），除非设定一个宽度。可以设置margin和padding属性。




元素的块和内联并不是固定的，只是根据默认属性划分的。可以通过 css 属性的 `display: inline` 将块级元素变成内联的，也可以通过`display: block` 将内联的元素变成块级显示。
 
#### 内联元素
内联元素特点：

1. 多个行内元素排成一行，直到一行排不下，才会换新一行；
2. 元素的高度、宽度及顶部和底部边距不可设置；不能设置width和height；
只可以设置水平方向的边距，如：margin-left,margin-right,padding-left,padding-right.
3. 元素的宽度就是它包含的文字或图片的宽度，不可改变。


#### 内联块状元素
display:inline-block
inline-block 元素特点：

1. 和其他元素都在一行上；
2. 元素的高度、宽度、行高以及顶和底边距都可设置。

inline-block{
简而言之就是让元素既可以在一行内显示，又可以设置宽高边距等。

}



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

##### 宽度和高度
盒模型宽度和高度和我们平常所说的物体的宽度和高度理解是不一样的，css内定义的宽（width）和高（height），指的是填充以里的内容范围。

因此一个元素实际宽度（盒子的宽度）=左边界+左边框+左填充+内容宽度+右填充+右边框+右边界。

![](/assets/539fbb3a0001304305570259.jpg)


##### 填充pandding 边界margin
元素内容与边框之间是可以设置距离的，称之为“填充”。填充也可分为上、右、下、左(顺时针)。如下代码：

div{padding:20px 10px 15px 30px;}

如果上、右、下、左的填充都为10px;可以这么写
div{padding:10px;}

如果上下填充一样为10px，左右一样为20px，可以这么写：
div{padding:10px 20px;}



