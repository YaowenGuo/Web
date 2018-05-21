# Embedded content

之前的标签都着重与文档的结构和意义。接下来的标签将丰富文档的内容。

> 元素速览

元素       |  说明                      |  类型   |   新增或有无变化  
--------- | ------------------------- | ------- | -------------  
area      | 表示一个用于客户端分区响应图的区域 | 短语 |  有变化
audio     | 表示一个音频资源             | 无      |  新增
canvas    | 生成一个动态的图形画布        | 短语、流 |  新增
embed     | 用插件在HTML中嵌入的内容      |  短语   |  新增
iframe    | 通过创建一个浏览上下文在一个文档中嵌入另一个文档。 | 短语 |  有变化
img       | 嵌入图像                    | 短语    | 有变化
map       | 定义客户端分区响应图          | 短语、流 | 有变化
meter     | 嵌入数值在许可范围背景中的图形表示| 短语   | 新增
object    | 在HTML文档中嵌入内容。也可以用于生成浏览上下文和生成客户端分区响应图 | 短语、流 |  有变化
param     | 表示将通过object元素传递给插件的参数 | 无 | 无变化
progress  | 嵌入目标进展或任务完成情况的图形表示 | 短语| 新增
source    | 表示媒体资源                | 无       |  新增
svg       | 表示结构化适量内容           | 无       |  新增
track     | 表示媒体的附加轨道（例如字幕） | 无       |  新增
video     | 表示视频资源                | 无       |  新增


## img 嵌入图像

元素      | img
-------  | ----
元素类型  | 短语元素
父元素    | 任何可能包含短语元素的元素
局部属性  | src、alt、height、width、usemap、ismap
内容     | 无
标签用法  | 虚元素形式
html新增  | 否
HTML5中变化 | border、longdesc、name、align、hspace和vspace属性在H5中已被废弃
默认样式   | 无

- src: 嵌入图像的URL
- alt: 图像无法显示时的备用显示内容。
- width、height: 图像的尺寸。图像在HTML处理完毕后才会加载，这意味着如果省略了width和height属性，浏览器就不知道为图像留出多大的屏幕空间。造成的结果是，浏览器必须依靠图像文件本省的尺寸来确定它的尺寸，然后重定位屏幕上的内容来容纳它。这可能让用户感觉到晃动。width和height属性来告诉浏览器图像的尺寸有多大，而不是你希望它有多大，不应该使用这些属性来动态缩放图像。
- ismap: 添加该属性，当img父元素为a标签时。给图像应用该属性给图像创建了分区响应图。图像的点击位置会附加到提交的URL上。

## map 创建客户端分区响应图

创建客户端分区响应图，当用户点击图像上的不同区域，可以让浏览器导航到不同的URL上。这一过程不需要通过服务器引导，因此需要使用元素来定义图像上的各个区域以及它们所代表的行为。

元素     | map
-------- | ----
元素类型  | 包含短语内容时时短语元素，包含流内容时被视为流元素
父元素    | 任何可以包含短语或流内容的元素
局部属性  | name
内容     | 一个或多个area元素。
标签用法  | 双标签
html新增  | 否
HTML5中变化 | 如果使用id属性，它的值必须与name属性值相同
默认样式   | 无

area 元素放在map元素内部，表示图像上可被点击的一块区域。

元素     | area
-------- | ----
元素类型  | 短语
父元素    | map元素
局部属性  | alt、href、target、rel、media、hreflang、type、shape、coords
内容     | 无
标签用法  | 虚元素形式
html新增  | 否
HTML5中变化 | rel、media和hreflang属性是HTML5中新增的。nohref已被废弃。
默认样式   | area {display: none; }

area 的属性可以分为两类，第一类处理的是area所代表的图像区域被用户点击后浏览器会导航到的URL。
- herf: 此区域被点击时，浏览器应该加载的URL
- alt: 无法显示图像时的代替内容
- target: 用来设置浏览器的上下文，跟a属性相同
- media: 此区域适用的媒介，与head中的style的media属性相同。
- hreflang: 目标文档的语言
- type: 目标文档的MIME类型。

另一类测包含了有意思的属性： shape和coords属性。可以用这些属性来标明用户点击的各个图形区域。shape和coords属性是共同其作用的。coords属性的意思根据shapes属性值而定。

- rect: 这个值代表了一个矩形区域。 coords 属性必须用由四个用逗号分隔的整数组成，它们代表了下列位置之间的距离：
    - 图像的左边缘与矩形的左侧
    - 图像的上上边缘与矩形的上侧
    - 图像的右边缘与矩形的右侧
    - 图像的下边缘与矩形的下侧
- circle: 这个值代表了一个圆形区域。 coords 属性必须由三个用逗号分隔的整数组成，他们代表了下列参数
    - 从图像左边缘到圆心的距离
    - 从图像上边缘到圆心的距离
    - 圆的半径
- poly: 这个值代表一个多边形。coords属性必须至少包含留个用逗号分隔的整数，每个对数字代表多边形的一个顶点。
- default: 这个值的意思是默认区域，即覆盖整张图片。shape属性使用这个值时不需要提供coords值。

```
<body>
    Here is a common form for representing the three activities in a triathlon.
    <p>
        <img src="triathlon.png" usemap="#mymap" alt="Triathlon Image"/>
    </p>
    The first icon represents swimming, the second represents cycling and the third
    represents running.

    <map name="mymap">
        <area href="swimpage.html" shape="rect" coords="3,5,68,62" alt="Swimming"/>
        <area href="cyclepage.html" shape="rect" coords="70,5,130,62" alt="Running"/>
        <area href="otherpage.html" shape="default" alt="default"/>
    </map>
</body>
```

注意 img 的usemap的值必须是一个井号串名称引用。

## iframe 嵌入另一张 HTML 文档

元素     | iframe
-------- | ----
元素类型  | 短语
父元素    | 任何可以包含短语内容的元素
局部属性  | src、srcdoc、name、width、height、sandbox、seamless
内容     | 字符数据
标签用法  | 双标签
html新增  | 否
HTML5中变化 | sandbox 和 seamless 属性是HTML5中新增的。未被列出属性已被废弃。
默认样式   | iframe {border: 2px inset; }


- width和height: 指定像素尺寸
- src: 指定ifram 一开始应该载入并显示的URL
- srcdoc: 定义一张内嵌显示的HTML文档
- seamless: 指示浏览器把ifram的内容显示得像住HTML的一个整体组成部分。
- sandbox: 对HTML文档进行限制，应用这个属性是如果不附带任何值，就会禁用键入的文档的：脚本、表单、插件、指向其他浏览器的上下文链接。另外，ifram的内容被视为与HTML文档的其余部分来源不同，这样会引发额外的安全措施。可以通过添加sandbox的属性值来独立启用各种功能。
    - allow-forms: 启用表单
    - allow-scripts: 启用脚本
    - allow-top-navigation: 允许链接指向顶层的浏览器上下文，这样就能用另一个文档替换当前整个文档，或者创建新的标签好窗口。
    - allow-same-origin: 允许iframe里的内容被视为与文档其余部分有同一来源位置。

## boject 通过插件嵌入内容
基本功各个具体属性基本具有，遇到相关使用时再行补充

## 嵌入数字表现形式

### profress 显示进度
用于表示某项任务逐渐完成的过程

元素     | progress
-------- | ----
元素类型  | 短语
父元素    | 任何可以包含短语内容的元素
局部属性  | value、max、form
内容     | 短语内容
标签用法  | 双标签
html新增  | 否
HTML5中变化 | 无
默认样式   | 无

- value: 当前进度。它位于0 和 max 之间的值。当max被省略是，范围是0和1之间。

### meter 显示范围里的值
显示某个范围内所有可能值中的一个。

元素     | meter
-------- | ----
元素类型  | 短语
父元素    | 任何可以包含短语内容的元素
局部属性  | value、min、max、low、hight、optimum、form
内容     | 短语内容
标签用法  | 双标签
html新增  | 否
HTML5中变化 | 无
默认样式   | 无

- max，min: 设置可能值所处的范围边界，它们可以可以用浮点数表示。
- meter 元素的显示可以分为三部分：过低、过高和最佳。low属性设置了一个值，在他之下的所有值都被认为是过低；hight值之上的所有值都被认为是过高； optinum属性则屎定了“最佳”值。


## 嵌入音频和视频

### audio 嵌入拼音

## canvas 嵌入图形
