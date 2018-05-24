# 文档元素

> 文档和元数据元素

用于常见html上层建筑，向浏览器说明文档的情况，定义脚本程序和css样式，提供浏览器禁用脚本是要显示扥内容。

head 除了包含用于说明 html 文档的元素，head 标签还能规定文档与外部资源（css样式文件）的关系、定义内嵌CSS样式，放置和载入脚本程序。

元素       |  说明                      |  类型   |   新增或有无变化  
--------- | ------------------------- | ------- | -------------  
DOCTYPE   | 表示HTML文档的开始          |   无     |  有变化
html      | 表示文档中HTML部分的开始     |   无     |  有变化
head      | 包含文档的元数据            |   无     |  无变化
title     | 设置文档的标题              |  元数据  | 无变化
base      | 设置相对URL的基础           |  元数据   | 无变化
link      | 定义与外部资源（通常是样式表或网站图表）的关系| 元数据 | 有变化
meta      | 提供有关文档的信息           | 元数据   | 有变化
script    | 定义脚本程序或外部脚本文件    |  元数据、短语  | 有变化
noscript  | 包含浏览器禁用脚本或者不支持脚本时显示的内容 | 元数据、短语 | 无变化
style     | 定义css样式或者外部样式文件   | 元数据   | 有变化
body      | 表示HTML文档的内容          |  无      | 有变化

## 文档三大部分

### DOCTYPE

告诉浏览器文档内容是 html 格式，第二标记 HTML的版本，html5中不再写版本信息。

### html 根元素

标明html的开始和结束。

元素    | html
------- | ----
元素类型 | 无
父元素   | 无
局部属性 | manifest（40章）
内容     | head 和 body 各一
标签用法  | 开始可结束标签，包含其他元素
html新增  | 否
HTML5中变化 | 新增 manifest 属性，html4中的属性不再使用
习惯样式   | html {display: block;} html:focus {outline: none;}


### head 包含元数据和文档信息

元素    | head
------- | ----
元素类型 | 无
父元素   | html
局部属性 | 无
内容     | 至少有一个title
标签用法  | 双标签
html新增  | 否
HTML5中变化 | 无
习惯样式   | 无

### body 包含文档内容

元素    | body
------- | ----
元素类型 | 无
父元素   | html
局部属性 | 无
内容     | 所有短语元素和流元素
标签用法  | 双标签
html新增  | 否
HTML5中变化 | 所有样式属性都不再使用，而是使用css实现
习惯样式   | body {display: block; margin: 8px} body:focus {outline: none;}


## head 内容元数据

元数据本身并不是文档内容，它提供了关于文档内容的信息。

```
<head>
</head>
```

### title 文档标题
用于显示在标题顶部和标签也得标签上。

元素    | title
------- | ----
元素类型 | 元数据
父元素   | head
局部属性 | 无
内容     | 文档标题
标签用法  | 双标签
html新增  | 否
HTML5中变化 | 无
习惯样式   | body {display: none;}

### base 相对URL的前缀
设置一个基准URL，让html中相对链接在此基础之上进行解析，base 还能设置链接在点击时的打开方式，以及提交表单时浏览器如何反应。

元素    | base
------- | ----
元素类型 | 元数据
父元素   | head
局部属性 | href,target
内容     | 无
标签用法  | 虚元素形式
html新增  | 否
HTML5中变化 | 无
习惯样式   | 无


- href: 基准url。如果没有设置，那么浏览器会将当前文档的URL认定为所有相对URL的解析基址。例如，假设浏览器从 http://myserver.com/app/mypage.html 载入了文档，该文档中有一个超链接的相对URL是 myotherpate.html, 那么点击这个超链接将从 http://myserver.com/app/yotherpate.html 这个绝对地址加载这个文档。

- target: 告诉浏览器如何打开文档，这个值代表浏览器的上下文。（8章 15章讲i 和 iframe 将会说明）

### 元数据说明文档

mete 元素用来定义文档的各种元数据。它有多种不同的用法，而且一个HTML文档可以包含多个meta元素。

元素    | meta
------- | ----
元素类型 | 元数据
父元素   | head
局部属性 | name、content、charset、http-equiv
内容     | 无
标签用法  | 虚元素形式
html新增  | 否
HTML5中变化 | 新增charset，http-equiv只能使用本小节的值，scheme被移除，也不再使用meta指定网页所使用的语言。
习惯样式   | 无

> 用法

1. 使用name/content 定义 名/值 元数据

```
<meta name="author" content="Adam Freman"/>
<meta name="description" content="A simple example">
```

常用的5个预定义元数据名称
- application name: 当前页面所属web系统的名称
- author: 当前页的作者
- generater: 用来生成HTML的软件名称
- keywords: 一批以逗号分开的字符串，用来描述字符串。
- robots: 告诉搜索引擎该如何处理该文档。noindex（不要索引本页）、noarchive（不要将本页存档或缓存）、nofllow（不要顺着本业的文档继续搜索下去）

更多的扩展元数据

2. 声明字符编码

```
<meta charset="utf-8">
```

3. http-equive模拟http标头字段

改写http标头字段的值，meta元素可以用来模拟和改写其中三种标头字段，

- refresh : 以秒为单位指定一个时间间隔，此时间过去之后，将从服务器从新载入该页面。也可以另外指定一个URL让浏览器载入，如 <meta http-equiv="refresh" content="5; https://www/baidu.com"。
- default-style: 指定页面优先使用的样式表。对应的content属性值应与同一文档中某个style元素或link元素的title属性值相同。
- content-type: 这是指定html编码的另一种用法。如<meta http-equiv="content-type" content="text/html; charset=UTF-8"/>

### style 定义CSS样式

定义HTML内嵌的样式（link元素则是导入外部样式表中的样式）。

元素    | style
------- | ----
元素类型 | 无
父元素   | 任何可包含元数据元素的元素，包括head、div、noscript、sction、artical、aside
局部属性 | type、media、scoped
内容     | CSS样式
标签用法  | 双标签
html新增  | 否
HTML5中变化 | scoped属性为HTML5新增
习惯样式   | 无

- type: 样式类型，目前浏览器支持吃css，所以值总是 `text/css`。
- scoped: 样式作用范围（尚无浏览器支持）。如果制定了scoped，那么其中的样式值作用于钙元素的父元素及所有兄弟元素；没有指定的话，将作用域整个文档。
- media: 指定样式适用的媒体。属性值有：
  - all： 所有媒体，默认属性。
  - aural： 语音合成器
  - braille：盲文设备
  - handheld：手持设备
  - progection：投影设备
  - print：打印预览和打印设备
  - screen：计算机显示屏幕
  - tty：电传打字机之类的等宽设备
  - tv：电视机

media 还有一些特性可以用来设计更具体的条件
```
<style type="text/css" media="screen AND (max-width: 500px)">
	a {
		background-color: gray;
		padding: 0.5em
	}
</style>
```

AND 用来组合设备和特性条件，除了AND，还可以用NOT和表示OR的逗号(,)，藉此可以为复杂而又具体的条件应用样式。


### 指定外部资源

css样式资源是最典型的情况之一

元素    | link
------- | ----
元素类型 | 元数据
父元素   | head、noscript
局部属性 | href、rel、hreflang、media、type、sizes
内容     | 无
标签用法  | 虚元素形式
html新增  | 否
HTML5中变化 | 新增size，原有的charset、rev、target属性在html5中不再使用。
习惯样式   | 无

### script 使用脚本

- 必须使用双标签

- 引用外部文件和内部嵌入代码不能写到同一个标签中，否则嵌入的内容会不执行。
