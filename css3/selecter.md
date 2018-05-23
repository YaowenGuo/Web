# 选择器

CSS3 在常规选择器的基础之上新增了属性选择器、伪类选择器、过滤选择器。可以帮助开发人员减少对HTML类名和ID名的依赖，以及对HTML元素的结构依赖。使编写代码更加简单轻松。CSS3的选择器在某些方面和jQuery选择器是完全一样的。

[TOC]

每一条css样式声明（定义）由两部分组成，形式如下：

选择器 {
    样式;
}

在{}之前的部分就是“选择器”，“选择器”指明了{}中的“样式”的作用对象，也就是“样式”作用于网页中的哪些元素。

> 选择器分类

根据所选择元素的不同，可以把CSS3的选择器分为5大类：

1. 基本选择器
2. 层次选择器
3. 伪类选择器
    1. 动态伪类选择器
    2. 目标伪类选择器
    3. 语言伪类选择器
    4. UI元素状态伪类选择器
    5. 结构伪类选择器
    6. 否定伪类选择器
4. 伪元素
5. 属性选择器

一共10种选择器

## 基本选择器
使用最多，也最久远。在css1中就定义了。

| 选择器    |   名称      |   作用对象    |    支持
| -------- | -----------| ------------ | ---------
| *        | 统配选择器   |  文档中的所有 HTML 元素 |
| E        | 元素选择器   | 对应名称的HTML元素      |
| #id_value| ID 选择器   | 指定ID属性值的为对应值的元素| 必须有HTML元素指定了响应的id值。具有唯一性，同一个文档中只能出现一次。
| .class_value| 类选择器 | 指定class属性值为对应值的的元素| .class1.class2~ 被称为多类选择器，只有一个元素同时具有所指定的所有类时，才会匹配。
| selector1, ... ,selectorN| 群组选择器 | 每一个选择器匹配的元素 | 选择器之间用逗号分隔，表示不同选择器。为了优雅，一般逗号后加一个空格分割。



- 类选择器使用点号 `.` 跟类名来表示区分。class 属性如其名字一样，是一类元素，class的名字应该是这类型的表示。不同的元素可以拥有形同的类名，表示它们是显示同一类内容的元素，或者同一类显示效果的元素。一个元素可以有多个类名，表示它从不同的角度，可以划分到不同的类别中去。

- 在使用样式进行操作时，应该将其样式类和功能类进行分开定义，这样在修改样式或功能需要修改时，如果需要修改类名，样式和功能彼此可以不相互影响。
- 只有多个元素拥有相同功能的的情况下才应该使用类名来关联js 实现功能。否则应该尽量使用 id 属性来给元素定义功能。这样功能和样式就能更好的分离。

- 类名不能是中文名，阿拉伯数字也不行

- id选择器在html标签中使用id属性定义 `<span id="stress">` 。id 标签只能使用一个命名，如下则是错误的。`<span id="stressid bigsizeid">`。设置两个将导致两个都失效。
- ID选择符的前面是井号（#）号，而不是英文圆点（.）。右侧代码编辑器中就是一个ID选择符的完整实例。


> 相同点与区别

相同点：可以应用于任何元素
不同点：

- W3C标准这样规定的，在同一个页面内，不允许有相同名字的id对象出现，但是允许相同名字的class。这样，一般网站分为头，体，脚部分，因为考虑到它们在同一个页面只会出现一次，所以用id，其他的，比如说你定义了一个颜色为red的class，在同一个页面也许要多次用到，就用class定义。另外，当页面中用到js或者要动态调用对象的时候，要用到id，所以要根据自己的情况运用。自己的语言

- 可以使用类选择器词列表方法为一个元素同时设置多个样式。我们可以为一个元素同时设多个样式，但只可以用类选择器的方法实现，ID选择器是不可以的（不能使用 ID 词列表）。



## 层次选择器
层次选择器通过HTML元素之间的关系获取元素，主要的层次关系包括：后代、负责、相邻兄弟和通用兄弟。通过这些关系可以减少类和id的定义，方便快捷的确定需要的元素。

层次选择器也是在CSS早期版本就有的，可以放心使用。

| 选择器    |   名称      |   作用对象    |    支持
| -------- | -----------| ------------ | ---------
| E F      | 后代断则气(包含选择器)|  选择器匹配包含在E元素之内的所有F指定的元素， | E 和 F 可以是除群组选择器之外的任意基本选择器
| E > F    | 子选择器    | 选择所有E元素的子元素并且符合F的指定| E 和 F 可以是除群组选择器之外的任意基本选择器
| E + F    | 相邻兄弟选择器 | 匹配紧跟在E元素之后的F元素，如果E和F元素之间有其他元素，那将不能匹配成功。
| E ~ F    | 通用兄弟选择器 | 匹配E元素后的所有符合F的元素。 |

 

- 子选择器使用 `>` 表示层级关系，在表示嵌套中使用的，父子选择器可以是任意类型。如
`.food>li{border:1px solid red;}`
会将class名为food下的子元素li（水果、蔬菜）加入红色实线边框。

注意子选择器不能跨越标签。如下则无法设置成功：
```
.first > span{
    border:1px solid red;
}

<p class="first">三年级时，<p>我还是一个<span>胆小如鼠</span>的小女孩</p>，上课从来不敢回答老师提出的问题，生怕回答错了老师会批评我。就一直没有这个勇气来回答老师提出的问题。学校举办的活动我也没勇气参加。</p>
```

- 子选择器，只工作于他的下一层代码，而不能控制当前层或者第三层；

- 包含选择器，即加入空格,用于选择指定标签元素下的后辈元素。 如 `.first  span{color:red;}`

`>` 作用于元素的第一代后代，空格作用于元素的所有后代。


## 伪类选择器

更有趣的是伪类选择符，为什么叫做伪类选择符，它允许给html不存在的标签（标签的某种状态）设置样式，比如说我们给html中一个标签元素的鼠标滑过的状态来设置字体颜色：
 `a:hover{color:red;}` 。上面一行代码就是为 a 标签鼠标滑过的状态设置字体颜色变红。这样就会使第一段文字内容中的“胆小如鼠”文字加入鼠标滑过字体颜色变为红色特效。

伪类选择器和其他选择器写法有明显的区别，都是以冒号开头加伪类名。如 `:hover`、`:click`等。

** 伪类元素是可以单独使用的，但是作用并不大。因为主要是用来表示用户对一些元素的操作的，不加其它选择器显示，会导致应用于所有的元素。**
如 `:hover {cursor: pointer; }` 将导致鼠标一直是一个小手的形状。

### 动态伪类选择器

动态伪类选择器在早期的CSS中就有。动态伪类选择器并不存在与HTML文档中，只有用户和网站交互的时候才能体现出来。动态伪类分为两种，一种是在链接中常看到的锚点伪类；另一种为用户行为伪类。

| 选择器    |   名称      |   作用对象    |    支持
| -------- | ----------- | ------------ | ---------
| E:link   | 链接伪类选择器| 匹配定义了超链接的E元素，常用于链接锚点上 | 当 a 链接内部是块元素时，无法包括，因此像背景色之类的外观元素无法响应。但是点击的响应范围和内部块元素一样大。感觉作用并不大，直接通过a元素就能匹配了。
| E:visited| 链接伪类选择器| 匹配被访问过的超链接E元素。| 还有那么点用
| E:active | 激活伪类选择器| 匹配被激活的元素E | 当点击鼠标时被激活,只有具有点击特点的元素才有改特性。如button、a
| E:hover  | 鼠标悬停伪类选择器 | 当元素E鼠标悬停时被激活。|
| E:focus  | 焦点伪类选择器 | 当元素E获得焦点时被激活 | 只有具有点击特点的元素才有改特性。如button、a
| E:checked| 选中伪类选择器 | 匹配元素选中时，主要用于input 元素|
| E:disabled| 禁用伪类选择器 | 被禁用时匹配，用于带有disable 属性的元素 |
| E:enabled | 可用伪类选择器 | 未被禁用时匹配，用于带有disable 属性的元素 |
| :valid | 内容合法选择器 | 当输入的内容合法时应用，主要用于input和textarea |
| :read-only | 只读伪类选择器 | 当input等设为只读时应用 |


一个可点击元素的状态有: 默认状态 -> 悬停状态 -> 点击状态 -> 焦点状态 -> 点击后状态

### 目标伪类选择器

只有一个

| 选择器    |   名称      |   作用对象    |    支持
| -------- | ----------- | ------------ | ---------
| E:target | 目标伪类选择器| 匹配所有匹配E并且有内部URL锚点指向的元素 | 匹配的元素一定是一个锚点，并且有URL指向该锚点。

设置锚点有两种方式

方法一：

①：设置一个锚点链接<a href="#miao">去找喵星人</a>；（注意：href属性的属性值最前面要加#）

②：在页面中需要的位置设置锚点<a name="miao"></a>；（注意：a标签中要写一个name属性，属性值要与①中的href的属性值一样，不加#）标签中按需填写必要的文字，一般不写内容

方法二：

①：同方法一的①

②：设置锚点的位置  <h3 id="miao">喵星人基地</h3>；在要跳转到的位置的标签中添加一个id属性，属性值与①中href的属性值一样，不加#

方法二不用单独添加一个a标签来专门设置锚点 ，只在需要的位置的标签中添加一个id即可。


### 结构伪类选择器

通过文档树结构的相互关系来匹配特定的元素，从而减少HTML文档对ID或类名的定义，帮助保持代码干净整洁。

所有的结构伪类选择器都是基于HTML文档树的，也成为文档对象模型（DOM）。它由元素、属性、文本组成的节点关系。

| 选择器    |   名称      |   作用对象    |    说明
| -------- | ----------- | ------------ | ---------
| E:first-child | 结构伪类选择器| 最为父元素第一个子元素的 E 元素 | 与 E:nth-child(1)等同。
| E:last-child  | 结构伪类选择器| 匹配 E 并且E是父元素最后一个子元素的元素 | 与 E:nth-last-child(1)等同。
| E:root   | 结构伪类选择器| 匹配 E 是文档的根元素的。在HTML文档中，根元素始终是html元素 | 与 html 标签选择器匹配内容等同。
| E F:nth-child(n)| 结构伪类选择器 | 选择父元素E的第n个子元素F | 其中n可以是整数（1、2、3）、关键字（enen、odd）、可以是公式（2n+1、-n+5），切n值起始值为1，而不是0
| E F:nth-last-child(n) | 结构伪类选择器 | 选择元素E的倒数第n个子元素F。 | 此选择器与`E F:nth-child(n)`的顺序相反，使用方法一致。
| E:nth-of-type(n) | 结构伪类选择器 | 父元素内具有指定类型的第n个E元素 |
| E:nth-last-of-type(n) | 结构伪类选择器 | 元素内具有指定类型的倒数第n个E元素 |
| E:first-of-type | 结构伪类选择器 | 父元素内具有指定类型的第1个E元素 | 与 E:nth-of-type(1)等同
| E:last-of-type | 结构伪类选择器 | 父元素内具有指定类型的最后一个E元素 | 与 E:nth-last-of-type(1)等同
| E:only-child   | 结构伪类选择器 | 选择E元素是父元素唯一子元素的E元素 |
| E:only-of-type | 结构伪类选择器 | 选择只包含一个同类型的子元素，且该子元素匹配E元素 |
| E:only-child   | 结构伪类选择器 | 选择没有子元素的元素，该元素也不包含任何文本节点 |

只有 `:first-child` 属于CSS2.1，其它都是CSS3新加的。

*** 注意: 伪类选择器是对选择器条件的补充，而不是下一级节点。例如 `li:last-child` 选择的是 li 元素，并且该元素是父元素的最后一个节点。如果li 并列的兄弟元素，最后一个不是 li, 那将无法匹配成功。 ***

```
<div>
    <ul>  <!-- ul:only-of-type -->
        <li>one</li> <!-- li:first-child 或 li:nth-child(2n+1) -->
        <li>two</li> <!-- li:nth-child(2) -->
        <li>three</li> <!-- li:last-child 或 li:nth-child(2n+1) -->
    </ul>
    <div>abc</div> <!-- div div:first-of-type -->
    <p>para</p>
    <div>def</div> <!-- div div:last-of-type -->
    <p>para</p> <!-- P:nth-of-type(2) -->
    <b>ghi</b>  <!-- b:only-of-type -->
</div>
```

> n 是什么

在选择器的括号中 `nth-child(n)`，`nth-last-of-type(n)`等，可以是什么值呢？n 为自然数或
`xn + 数字` 的形式。但是元素是从 1 开始的。所以，当计算结果小于等于0时，将匹配不到元素。

还可以为 odd (表示奇数)，even（表示偶数）


### 否定伪类选择器语法

:not() 是一个非常强大有用的选择器，用于过滤一些特殊条件下，选择剩余的元素。not中的内容也可以多种多样，可以是基本HTML元素，例如除了div之外的匹配元素
`:not(div) {...}`

可以是属性值，例如选中处理raddio类型的input的元素
`input:not([type=submit]){...}`

可以是其他伪类选择器，例如除了第一个元素
`tabel th:not(:first-type-child){...}`

`.gallery:hover li:not(:hover){...}`


### 伪元素

CSS3还可以定位伪元素，伪元素可用于定位文档中包含的文本，但无法在文档树中定位。伪类一般反应无法在CSS中轻松活可靠的检测到的某个元素属性或状态；另一方面，伪元素表示DOM外部的某种文档结构。

伪元素使用双冒号表示。用于区分伪类。

| 选择器    |   名称      |   作用对象    |    说明
| -------- | ----------- | ------------ | ---------
| ::after  |             | 
| ::before |             |
| ::first-letter |       | 选择文本块的第一个字母，除非在块之前包含有其他元素。|  经常会有一些排版将一段文字的第一个字母放大。
| ::first-line |         | 匹配第一行文本 | `::first-line` 将匹配block、inline-block、teble-caption、table-cell等级别元素额第一行。
| ::selection |          | 用来匹配突出显示的文本。| 对于选中的文本，浏览器默认是蓝底白字，想要设计与众不同的效果，`::selection`非常有用。


::before 和 ::after 不是指存在于标记中的内容，而是可以插入额外内容的位置。尽管生成的内容不会称为DOM中的一部分。但它同样可以设置样式。

要为伪元素生成内容，还需要配饰content属性。例如，假设在页面上所有外部链接之后的括号中附加它们所指像的URL，无序将URL硬编码到标记中，可以结合使用一个属性选择器和`::after`伪元素
```
a[hred^=http]::after {
    content:"(" attr(href) ")";
}
```
还可以给链接加icon。


## 属性选择器

| 选择器    |   作用对象    |    说明
| -------- | ------------ | ---------
| E[attr]   | 具有属性的元素，E可以省略，表示任意具有attr属性的元素 。 |
| [attr=val] | attr属性值设置为val（val区分大小写）的元素 |
| `[attr|=val]`| attr属性值是val或是以val-开头的元素 |
| [attr~=val]| attr属性值被设置为多个值，其中一个值为val |
| [attr*=val]| attr属性值任意位置包含了val的元素 |
| [attr^=val]| attr属性是以val开头的任意字符串的元素 |
| [attr$=val]| attr属性值设置了以val结尾的元素 |


- 属性选择器可以单独使用，表示任意具有改属性的元素。也可以和元素一起使用，使用的格式是`E[attr][attr1]....`，可以多个属性一起筛选。