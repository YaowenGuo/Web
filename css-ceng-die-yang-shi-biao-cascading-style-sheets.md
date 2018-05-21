主要是用于定义HTML内容在浏览器内的显示样式，如文字大小、颜色、字体加粗等。

使用CSS样式的一个好处是通过定义某个样式，可以让不同网页位置的文字有着统一的字体、字号或者颜色等。
#### css 位置
例如给html的某个标签加样式，直接在<style type="text/css"> 中编写。例如给标签p添加样式。
```html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>认识CSS样式</title>
<style type="text/css">
p{
   font-size:20px;/*设置文字字号*/
   color:red;/*设置文字颜色*/
   font-weight:bold;/*设置字体加粗*/
}
</style>
</head>
<body>
<p>测试文字！</p>
</body>
</html>
```

##### 内联式
内联式css样式表就是把css代码直接写在现有的HTML标签中，如下面代码：
```css
<p style="color:red">这里文字是红色。</p>
注意要写在元素的开始标签里，下面这种写法是错误的：
<p>这里文字是红色。</p style="color:red">
并且css样式代码要写在style=""双引号中，如果有多条css样式代码设置可以写在一起，中间用分号隔开。如下代码：
<p style="color:red;font-size:12px">这里文字是红色。</p>
```

css 样式由选择符和声明组成，而声明又由属性和值组成，如下图所示：

![](/assets/52fde5c30001b0fe03030117.jpg)
##### 嵌入式
嵌入式是使用单独的<style type="text/css"> </style> 标签内写样式。例如给span标签加样式。
```css
<style type="text/css">
span{
color:red;
}
</style>
```
嵌入式css样式必须写在<style></style>之间，并且一般情况下嵌入式css样式写在<head></head>之间。如右边编辑器中的代码。
##### 外部css样式，单独写在一个文件中
在<head>内（不是在<style>标签内）使用<link>标签将css样式文件链接到HTML文件内，如下面代码：
<link href="base.css" rel="stylesheet" type="text/css" />

注意：

1、css样式文件名称以有意义的英文字母命名，如 main.css。

2、rel="stylesheet" type="text/css" 是固定写法不可修改。

3、<link>标签位置一般写在<head>标签之内。

##### 三种方法的优先级
距离越近，优先级越高。所以
内联式 > 嵌入式 > 外部式
当属性在不同优先级重复时，优先级高的有效。

但是嵌入式>外部式有一个前提：嵌入式css样式的位置一定在外部式的后面。如右代码编辑器就是这样，<link href="style.css" ...>代码在<style type="text/css">...</style>代码的前面（实际开发中也是这么写的）。感兴趣的小伙伴可以试一下，把它们调换顺序，再看他们的优先级是否变化。
例如如下的写法将导致外部优先：

```
<style type="text/css">

    span{
       color:red;
    }
</style>
<link href="style.css" rel="stylesheet" type="text/css">
```
但注意上面所总结的优先级是有一个前提：内联式、嵌入式、外部式样式表中css样式是在的相同权值的情况下，什么是权值呢？

1.  内联样式表的权值最高 1000

2.  ID 选择器的权值为 100

3.  Class 类选择器的权值为 10

4.  HTML 标签选择器的权值为 1

CSS 优先级法则：

A  选择器都有一个权值，权值越大越优先

B  当权值相等时，后出现的样式表设置要优于先出现的样式表设置

C  创作者的规则高于浏览者：即网页编写者设置的CSS 样式的优先权高于浏览器所设置的样式

D  继承的CSS 样式不如后来指定的CSS 样式

E  在同一组属性设置中标有“!important”规则的优先级最大

这是规定好的,自然不能打破

#### 注释

用/*注释语句*/