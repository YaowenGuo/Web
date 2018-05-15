# form 表单

[TOC]

表单是HTML中获取用户输入的手段，它对于Web应用系统及其重要，然而HTML定义的功能落后于表单的使用方式已有多年。在HTML5中，整个表单系统已经彻底改造，面貌焕然一新，标准的步伐已经跟上了表单的应用步伐。

新引入的特性
- 从用户收集特定类型数据的新方法
- 在浏览器中检查数据

主流浏览器对HTML5表单的支持已经很不错了，但是算不上完美。使用时应该先检查该表单特性是否已经得到广泛的支持。

> 元素一览

元素       |  说明                      |  类型   |  新增或有无变化  
--------- | -------------------------- | ------ | -------------  
form      | 表单                       |   流    |  有变化
button    | 按钮（不局限于在表单中使用）   |  短语    |  有变化
input     | 输入框                     |  短语    |  有变化
textarea  | 多行输入的文本区             |  短语    |  有变化
datalist  | 定义一组提供给用户的建议值     |  流     |  有变化
fieldset  | 表示一组表单元素             |   流    |  有变化
keygen    | 生成一对公钥和私钥           |  短语    |  新增
label     | 表示表单元素的说明           |  短语    |  有变化
ledend    | 表示fieldset的说明          |   无    |  无变化
optgroup  | 表示一组相关的option元素     |   无    |  无变化
option    | 表示提供用户选择的一个选项    |   无     |  无变化
output    | 表示计算结果                |  短语    |  新增
select    | 给用户提供一组固定的选项      |  短语    |  有变化


> 跟表格table一样，表单元素基本的元素也是三个，form、input、button。

## form 表单元素

元素      | form
-------- | ----
元素类型  | 流
父元素    | 任何可以包含流的元素，但form不能是其他form的后代。
局部属性  | action、mathod、enctype、name、accept-charset、novalidate、target、autocomplete
内容     | 流内容（但主要是是label元素和input元素）
标签用法  | 双标签
html新增  | 否
HTML5中变化 | 新增novalidate和autocomplate 属性
默认样式   | form {display: block; margin-top: 0em; }

> form 属性

- action: 指定在提交表单数据时，应该把用户的数据发送到什么地方。如果没有设置，浏览器将会把数据发送到当前文档的URL。

- method: http 请求方法。默认是get方法

- enctype: 浏览器发送给服务器的数据使用的编码方式。改属性值有三个
    - application/x-www-form-urlencoded: 这是未设置enctype属性时使用的默认编码方式。它不能将文件上传到服务器。它会以 `fave=Apple&name=Adam` 的格式传输数据。没项数据的名称和值都与URL采用相同的编码方案。

    - text/plain: 该编码因浏览器而异。这种编码要谨慎使用。测试已经在Chrome、Firefox、Safari已完全一样。将`application/x-www-form-urlencoded` 中的 `&` 编程了用换行分割而已。即每个数据占用一行。

    - multipart/form-data: 用于将数据和文件等混合数据发送到服务器。它更冗长，处理起来也更复杂，这也是它一般只用于上传文件到服务器的的表单的原因。

```
------WebKitFormBoundaryRRix1v33ZtHqE9WV
Content-Disposition: form-data; name="fave"

Apple
------WebKitFormBoundaryRRix1v33ZtHqE9WV
Content-Disposition: form-data; name="name"

Adam
------WebKitFormBoundaryRRix1v33ZtHqE9WV--
```

- autocomplate: 浏览器能够记住用户输入的内容，在用户再次输入时，会有个列表，用于自动补全用户的输入。不过有时候，网页的作者并不想让浏览器自动补全。只需要将该属性设置为off即可。
    - input 元素也有autocomplate，这样就能更灵活的控制表单的补全功能。

- target: 指定表单反馈信息的位置。改属性与a元素的target属性一致。默认情况下回用反馈信息替换原页面。
    - `_blank`: 新窗口中显示。
    - `_parent`: 在父窗框组中。
    - `_self`: 当前窗口（默认）
    - `_top`: 在顶层窗口中。
    - `<frame>`: 显示在指定窗框助中

- name: 为表单设置一个独一无二的标识符。以便使用DOM时区分各个表单。name属性与全局属性id不是一回事。后者在HTML文档中多用于css选择器。提交时该name值并不会上传到服务器，作用仅限于DOM中。而input元素不设置name属性，则这个输入就不会被发送到服务器。



## input 用户输入
元素      | input
-------- | ----
元素类型  | 短语元素
父元素    | 任何可以包短语元素的元素
局部属性  | name、disabled、form、type，以及取决于type属性的其他一些属性
内容     | 无
标签用法  | 虚元素形式
html新增  | 否
HTML5中变化 | type类型有增加。此外还添加了一些新的属性，他们需要与type属性的特定值搭配使用。
默认样式   | 无，元素样式取决于type属性。

input元素的属性多大29个，具体哪些可用取决于type属性的值。
- autofocus: 在页面打开时，输入自动聚焦到该元素。如果有多个被标记，将聚焦到最后一个元素上。
- disabled: 禁用输入或点击。
- type: 用于设置输入的不同检查数据类型。改属性有23个不同的值。在将type设置为想要的值之后，又有一些额外的属性可以搭配使用。该元素一共有30个属性值。
    - text: 文本。默认属性值。可以关联使用的属性有：dirname、list、maxlength、pattern、placeholder、readonly、required、size、value
    - placeholder: 背景提示
    - submit, reset, button: 作为按钮使用。它们可用的属性和 button 元素相同。
    - password: 隐藏用户输入的内容。可以配合使用的属性值：maxlength、pattern、placeholder、readlonly、required、size、value
    - number: 只能输入数字（整数或浮点数甚至科学计数法）。可以使用的额外属性：list、min、max、readlonly、required、step、value。
    - email: 邮箱格式
    - tel: 电话号码
    - url: 完全限定的 url 格式
    - datatime: 带时区信息的世界时（包括日期和时间）
    - datatime-local: 不带时区信息的世界时（包括日期和时间）
    - date: 日期
    - month: 年和月
    - time: 时间
    - week: 年及星期
    - color: 颜色
    - range: 将输入内容限制在一个数值范围内。
    - checkbox: 作为只能选择是否的输入类型
    - radio: 作为多选一的单选输入类型
    - radiobutton: 将输入限制为一组固定选项中进行选择。
    - search: 搜索类型
    - hidden: 隐藏
    - image: 上传图片
    - file: 上传图片， 并将form的 enctype 属性设置为 multipart/form-data
- dirname: 指定内容文字方向。该属性值同样会传输到服务器。Firefox还不支持。
- list: 关联提示列表datalist元素的id
- size: 通过指定文本框中可见的字符数目设置其宽度（英文字母数量）
- maxlength: 文本框中输入的字符的最大数目
- value: 初始的默认值
- readonly: 只读以组织用户编辑其内容。不会改变外观。应该慎重使用这个元素，因为看起来没有什么不同，却不能编辑，这会让用户迷惑。
- disabled: 禁用输入框。显示为灰色，并且不会被提交。如果想要提交，应该考虑使用hedden型input元素。
- pattern: 指定一个用于输入验证的正则表达式
- required: 表示用于必须输入一个值，否则无法通过验证
- placeholder: 设置一段提示文字告诉用户应该输入什么类型的数据
- min: 可以接受的最小值
- max: 可以接受的最大值
- step: 上下调节数值的步长


## button 表单的提交和重置

当用户将表单的内容全部填写完毕之后，需要把他们发送给服务器了。这个事情需要一个操作提醒，多半使用button来做的。如果使用button来完成提交。button不需要写任何代码，浏览器自动为表单中的button绑定了一个操作。即：当点击button之后，浏览器将收集表单中的所有数据，组织成固定格式，发送给form元素的 action 属性所指定的地址。这就是使用form表单提交数据的方便之处。不方便的地方是：你需要知道组织数据的方法和获取方式。

元素      | button
-------- | ----
元素类型  | 短语元素
父元素    | 任何可以包短语元素的元素。不仅限于在form中。
局部属性  | name、disabled、form、type，value、autofocus，以及取决于type属性的其他一些属性
内容     | 短语内容
标签用法  | 双标签
html新增  | 否
HTML5中变化 | 新增了一些熟悉，具体有哪些属性取决于type属性的值。
默认样式   | 无

## label 添加提示信息

用于给输入框添加提示信息。

元素      | label
-------- | ----
元素类型  | 短语元素
父元素    | 任何可以包短语元素的元素。不仅限于在form中。
局部属性  | for、form
内容     | 短语内容
标签用法  | 双标签
html新增  | 否
HTML5中变化 | form 属性为H5新增
默认样式   | label {cursor: default; }

- for: 设置为对应input的id值。这样使label和input的关系更加灵活。可以嵌套也可以并列。


## fieldset 对表单元素分组
对于复杂的表单，有时需要将一些元素组织在一起，可以使用fieldset元素。

元素      | fieldset
-------- | ----
元素类型  | 流元素
父元素    | 任何可以包流元素的元素。通常是form元素及其后代元素。
局部属性  | name、form、disabled
内容     | 流内容，在开头位置可以包含一个legend元素。
标签用法  | 双标签
html新增  | 否
HTML5中变化 | form 属性为H5新增
默认样式   | fieldset {display: block; margin: 2px 0.35em; padding: 0.35em 0.75em 0.625em 0.75em; border: 2px groove; }

- disabled: 禁用整组输入。

## legend 为 fieldset 添加说明标签

在分组之后，还可以给每个分组有一个提示，它会像标题一样显示在分组顶部。legend 必须是 fieldset 的第一个子元素。

元素      | legend
-------- | ----
元素类型  | 无
父元素    | fieldset
局部属性  | 无
内容     | 短语内容
标签用法  | 双标签
html新增  | 否
HTML5中变化 | 无
默认样式   | legend {display: block; panding-start: 2px; panding-end: 2px; border: none; }

## button 按钮

button不仅可以用在表单中，还可以用在表单之外，作为普通button使用。button的type属性支持三种值，其中submit和reset用于表单中。而button则用于表单之外作为普通的button使用。

- submit: 提交表单（默认）。使用该属性时可以使用的其他属性(H5新增)，这些属性看起来用处并不明显，然而在需要将表单数据提交到不同地址时，确是最简单的方法。
    - form: 指定按钮关联的表单的id。有了该属性，button甚至可以放在form之外提交表单（H5的改变）。input元素也具有这种性质。
    - formaction: 覆盖form元素的action属性，另行指定表单将要提交到的URL。
    - formenctype: 覆盖form元素的enctype属性，另行指定表单的编码方式。
    - formmethod: 覆盖form元素的method属性。
    - formnovalidate: 覆盖form元素的 novalidate 属性，表示是否执行客户端数据有效性检查。

- reset: 重置表单，即清空为初始化状态。没有额外属性。
- button: 用于表单之外作为普通按钮使用。可以包含任意短语元素。

## datalist 数据列表

将 input 元素的list属性值设置为 datalist 元素的 id 值。这样用户在输入时就能从选项中快速选择作为输入。

```
<!DOCTYPE HTML>
<html>
    <head>
        <title>Example</title>
        <meta name="author" content="Adam Freeman"/>
        <meta name="description" content="A simple example"/>
        <link rel="shortcut icon" href="favicon.ico" type="image/x-icon" />
    </head>
    <body>        
        <form method="post" action="http://titan:8080/form">
            <p>
                <label for="name">
                    Name: <input placeholder="Your name" id="name" name="name"/>
                </label>
            </p>
            <p>
                <label for="city">
                    City: <input placeholder="Where you live" id="city" name="city"/>
                </label>
            </p>            
            <p>
                <label for="fave">
                    Fruit: <input list="fruitlist" id="fave" name="fave"/>
                </label>
            </p>
            <button type="submit">Submit Vote</button>
        </form>

        <datalist id="fruitlist">
            <option value="Apples" label="Lovely Apples"/>
            <option value="Oranges">Refreshing Oranges</option>
            <option value="Cherries"/>
        </datalist>

    </body>
</html>
```

包含在 datalist 元素中的每一个option 元素都代表一个供用户选择的值。其value 属性值在该元素代表的选项被选中时，就是input所用的数据值。
- 显示在value列表中的未必就是value的属性值，还可以是另外设定的一条说明信息，它可以用label属性设置，也可以作为option的内容。但是这在不同浏览器下的显示效果存在很大不同，而且，显示的内容和选中后填入input内的值不一样，很容易引起用户的疑惑。
