# table

用于以网格的形式显示二维数据。在HTML的早期版本中，用表格空格页面布局的现象很常见。现在已经不再允许这样做，取而代之的是新增的CSS表格特征。

[TOC]

> 元素一览

元素       |  说明                      |  类型   |  新增或有无变化  
--------- | -------------------------- | ------ | -------------  
table     | 表格                       |   流    |  有变化
caption   | 标题                       |   无    |  有变化
thead     | 标题行                     |   无    |  有变化
th        | 表格                       |   无    |  有变化
tbody     | 表主体                     |   无    |  有变化
tfoot     | 表脚                       |   无    |  有变化
tr        | 一行                       |   无    |  有变化
col       | 一列                       |   无    |  有变化
colgroup  | 一组列                     |   无    |  有变化
td        | 单元格                     |   无    |  有变化

创建一个表格，table、tr、td是必须有的。table是HTML支持表格式布局的核心元素。

***table 标签到 td 标签之间不能插入非表格元素。否则会莫名其妙的消失了，其实是被浏览器过滤掉了。***

# table 表格

元素     | table
------- | ----
元素类型 | 流
父元素   | 任何可以包含流的元素
局部属性 | border
内容     | 以上表格内元素
标签用法  | 双标签
html新增  | 否
HTML5中变化 | summary、align、width、bgcolor、cellpadding、cellspacing、frame和rules属性已不再使用，其功能由css实现，border 属性的值必须设置为1。表格边框的粗细必须用CSS控制。
默认样式   | table {display: block; border-collapse: separate; border-spacing: 2px; border-color: gray; }

- border 使用设个属性用来告诉浏览器，这个表格是用来表示表格式数据，而不是用来布局的。大多数浏览器见到这个属性时，都会在表格和每个单元格周围绘制出边框。其值必须为1或空字符串“”。改属性并不控制样式，那是css的工作。


## tr 行 td 列

HTML基于行而不是列，每个行必须分别标记。

元素     | tr
------- | ----
元素类型 | 无
父元素   | table、thead、tfoot、tbody
局部属性 | 无
内容     | 一个或多个td或th元素。
标签用法  | 双标签
html新增  | 否
HTML5中变化 | align、char、charoff、valign和bgcolor属性已不再使用，其功能由css实现。
默认样式   | tr {display: table-row; vertical-align: inherit; border-color: inherit; }

元素     | td 单元格
------- | ----
元素类型 | 无
父元素   | tr
局部属性 | colspan、rowspan、headers
内容     | 流内容。
标签用法  | 双标签
html新增  | 否
HTML5中变化 | 其余属性已不再使用
默认样式   | td {display: table-cell; vertical-align: inherit; }

*** 有了三个核心元素，就能组装出表格。 ***

> 但是为了让表格内容根据语义化，常需要以下的元素

## th 表头单元格

元素     | td 单元格
------- | ----
元素类型 | 无
父元素   | tr
局部属性 | colspan、rowspan、headers
内容     | 短语内容
标签用法  | 双标签
html新增  | 否
HTML5中变化 | 其余属性已不再使用
默认样式   | td {display: table-cell; vertical-align: inherit; font-weight: bold; text-align: center; }

td,th都有header属性，header属性值可以设置为一个或多个表头th的id属性值，用于说明该单元格关联到某行某列。它可以供屏幕阅读器和其它残障辅助技术用来简化对表格的处理。

## 划分表格内容
结构化的数据不仅设置语义清晰，设置样式也变得灵活，而且根据结构添加的样式不会因为添加数据和减少数据而变得错乱。

表格可以细分为表主体、表头、表脚。表主体是包含数据的地方。
### tbody表主体
元素     | tbody, thead, tfoot
------- | ----
元素类型 | 无
父元素   | table
局部属性 | 无
内容     | 零个或多个tr元素
标签用法  | 双标签
html新增  | 否
HTML5中变化 | 原有属性都被废弃. tfoot 现在出现在 tbody，tr前后都可以。
默认样式   | tbody {display: table-row-group; vertical-align: middle; border-color: inherit; }
默认样式   | thead {display: table-header-group; vertical-align: middle; border-color: inherit; }
默认样式   | tfoot {display: table-footer-group; vertical-align: middle; border-color: inherit; }

> 即便在文档表格中没有用到table元素，大多数浏览器在处理table元素时，都会自动插入tbody元素，因此完全根据文档中的表格结构设计的css选择器可能不管用。例如，由于浏览器在table和tr之间插入了tbody元素。table > tr 选择器会失效。需要使用table > tbody > tr 或者 table tr。 甚至可以使用 tbody > tr 选择器。

不要让两个单元格扩展到同一区域从而形成重叠单元格。表格元素的用途是表格式数据。形成重叠单元格的唯一原因是表格元素布局其他元素，而这个特性应该用CSS的表格特性来做。

## caption 为表格添加标题

为表格定义一个标题，并将其与表格关联起来。

元素     | caption
------- | ----
元素类型 | 无
父元素   | tr
局部属性 | 无
内容     | 流，但不能是table元素
标签用法  | 双标签
html新增  | 否
HTML5中变化 | align余属性已不再使用
默认样式   | caption {display: table-caption; text-align: center; }

## calgroup,col 处理列

HTML 中表格是基于行的，即元素都是放在tr元素中，一行一行地组件起来的。因此对于列的应用样式有点不方便，对于包含不规则单元格的表格更是如此。colgroup和col正是用于解决这个问题。colgroup代表一组列。


```html5
<table border="1">
	<caption>Table Deme</caption>
	<colgroup id="colgroup1">
		<col id="col1And2" span="2" />
		<col id="col3"/>
	</colgroup id="colgroup2" span="2">
	<colgroup></colgroup>
	<thead>
		<tr><th>Rand</th><th>Name</th><th>Color</th><th colspan="2">Size & Votes</th></tr>
	</thead>
	<tbody>
		<tr>
			<th>Favorite:</th><td>Apple</td><td>Green</td><td>Medium</td><td>500</td>
		</tr>
		<tr>
			<th>2nd Favorite:</th><td>Oranges</td><td>Orange</td><td>Large</td><td>450</td>
		</tr>
		<tr>
            <th>3rd Favorite:</th><td>Pomegranate</td>
            <td colspan="2" rowspan="2">
                Pomegranates and cherries can both come in a range of colors
                and sizes.
            </td>
            <td>203</td>
        </tr>
        <tr>
            <th rowspan="2">Joint 4th:</th>
            <td>Cherries</td>
            <td rowspan="2">75</td>
        </tr>
        <tr>
            <td>Pineapple</td>
            <td>Brown</td>
            <td>Very Large</td>
         </tr>
	</tbody>
	<tfoot>
		<tr><th colspan="5">&copy; 2011 Adam Freeman Fruit Data Enterprises</th></tr>
	</tfoot>
</table>
```
