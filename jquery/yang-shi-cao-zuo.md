# 节点操作》
### 添加和改变节点内容 .html() text()
# *** Jquery 对设置和获取进行了优化，并不是通过函数名来区分设置和获取，而是通过重载，不传参的就是获取 ***

1. .text/.html() 不传入值，就是获取集合中第一个匹配元素的HTML内容
2. .text/.html( htmlString )  设置每一个匹配元素的html内容
3. .text/.html( function(index, oldhtml) ) 用来返回设置HTML内容的一个函数

获取集合中  ***第一个*** 匹配元素的HTML内容
 或 设置 ***每一个*** 匹配元素的html内容。

> 异同
1. html与.text的方法操作是一样，只是在具体针对处理对象不同

2. .html处理的是元素内容，.text处理的是文本内容
3. .html只能使用在HTML文档中，.text 在XML 和 HTML 文档中都能使用
4. 如果处理的对象只有一个子文本节点，那么html处理的结果与text是一样的
5. 火狐不支持innerText属性，用了类似的textContent属性，.text()方法综合了2个属性的支持，所以可以兼容所有浏览器
6. html()匹配的是元素本身，而text（）匹配元素集合中每个元素的文本内容结合，包括他们的后代。例如:

```
<div class="div">
    <a>:first-child</a>
    <a>第二个元素</a>
    <a>:last-child</a>
</div>

$(".div").html() 获取的是
<a>:first-child</a>
<a>第二个元素</a>
<a>:last-child</a>
而$(".div").text() 获取的是
":first-child
第二个元素
:last-child
"

```

.html()方法内部使用的是DOM的innerHTML属性来处理的，所以在设置与获取上需要注意的一个最重要的问题，这个操作是针对整个HTML内容（不仅仅只是文本内容）


> function(index,text) 返回的是

### 表单样式的值

.val()方法主要是用于处理表单元素的值，比如 input, select 和 textarea。

.html(),.text()和.val()的差异总结：  

1. .html(),.text(),.val()三种方法都是用来读取选定元素的内容；只不过.html()是用来读取元素的html内容（包括html标签），.text()用来读取元素的纯文本内容，包括其后代元素，.val()是用来读取表单元素的"value"值。其中.html()和.text()方法不能使用在表单元素上,而.val()只能使用在表单元素上；另外.html()方法使用在多个元素上时，只读取第一个元素；.val()方法和.html()相同，如果其应用在多个元素上时，只能读取第一个表单元素的"value"值，但是.text()和他们不一样，如果.text()应用在多个元素上时，将会读取所有选中元素的文本内容。

2. .html(htmlString),.text(textString)和.val(value)三种方法都是用来替换选中元素的内容，如果三个方法同时运用在多个元素上时，那么将会替换所有选中元素的内容。

3. .html(),.text(),.val()都可以使用回调函数的返回值来动态的改变多个元素的内容。



### 属性与样式之.attr()与.removeAttr()
每个元素都有一个或者多个特性，这些特性的用途就是给出相应元素或者其内容的附加信息。如：在img元素中，src就是元素的特性，用来标记图片的地址。

操作特性的DOM方法主要有3个，getAttribute方法、setAttribute方法和removeAttribute方法，就算如此在实际操作中还是会存在很多问题，这里先不说。而在jQuery中用一个attr()与removeAttr()就可以全部搞定了，包括兼容问题

jQuery中用attr()方法来获取和设置元素属性,attr是attribute（属性）的缩写，在jQuery DOM操作中会经常用到attr()

attr()有4个表达式

attr(传入属性名)：获取属性的值
attr(属性名, 属性值)：设置属性的值
attr(属性名,函数值)：设置属性的函数值
attr(attributes)：给指定元素设置多个属性值，即：{属性名一: “属性值一” , 属性名二: “属性值二” , … … }
removeAttr()删除方法

.removeAttr( attributeName ) : 为匹配的元素集合中的每个元素中移除一个属性（attribute）

优点：

attr、removeAttr都是jQuery为了属性操作封装的，直接在一个 jQuery 对象上调用该方法，很容易对属性进行操作，也不需要去特意的理解浏览器的属性名不同的问题

注意的问题：

dom中有个概念的区分：Attribute和Property翻译出来都是“属性”，《js高级程序设计》书中翻译为“特性”和“属性”。简单理解，Attribute就是dom节点自带的属性

例如：html中常用的id、class、title、align等：

<div id="immooc" title="慕课网"></div>
而Property是这个DOM元素作为对象，其附加的内容，例如,tagName, nodeName, nodeType,, defaultChecked, 和 defaultSelected 使用.prop()方法进行取值或赋值等

获取Attribute就需要用attr，获取Property就需要用prop
```
 <script type="text/javascript">
    	//找到第一个input，通过attr设置属性value的值
    	$("input:first").attr('value','.attr( attributeName, value )')
    </script>

    <script type="text/javascript">
    	//找到第二个input，通过attr获取属性value的值
    	$("input:eq(1)").attr('value')
    </script>

    <script type="text/javascript">
    	//找到第三个input，通过使用一个函数来设置属性
    	//可以根据该元素上的其它属性值返回最终所需的属性值
    	//例如，我们可以把新的值与现有的值联系在一起：
    	$("input:eq(2)").attr('value',function(i, val){
    		return '通过function设置' + val
    	})
    </script>

    <script type="text/javascript">
    	//找到第四个input，通过使用removeAttr删除属性
    	$("input:eq(3)").removeAttr('value')
    </script>
```

### 改变类名
当一个节点（或称为一个标签）含有多个class时，DOM元素响应的className属性获取的不是class名称的数组，而是一个含有空格的字符串，这就使得多class操作变得很麻烦。同样的jQuery开发者也考虑到这种情况，增加了一个.addClass()方法，用于动态增加class类名

1. .addClass( className ) : 为每个匹配元素所要增加的一个或多个样式名
2. .addClass( function(index, currentClass) ) : 这个函数返回一个或更多用空格隔开的要增加的样式名


.removeClass( )方法

1. .removeClass( [className ] )：每个匹配元素移除的一个或多个用空格隔开的样式名
2. .removeClass( function(index, class) ) ： 一个函数，函数返回值，返回一个或多个将要被移除的样式名

注意事项

如果一个样式类名作为一个参数,只有这样式类会被从匹配的元素集合中删除 。 如果没有样式名作为参数，那么所有的样式类将被移除

> 互斥切换

在做某些效果的时候，可能会针对同一节点的某一个样式不断的切换，也就是addClass与removeClass的互斥切换，比如隔行换色效果

jQuery提供一个toggleClass方法用于简化这种互斥的逻辑，通过toggleClass方法动态添加删除Class，一次执行相当于addClass，再次执行相当于removeClass

.toggleClass( )方法：在匹配的元素集合中的每个元素上添加或删除一个或多个样式类,取决于这个样式类是否存在或值切换属性。即：如果存在（不存在）就删除（添加）一个类

.toggleClass( className )：在匹配的元素集合中的每个元素上用来切换的一个或多个（用空格隔开）样式类名
.toggleClass( className, switch )：一个布尔值，用于判断样式是否应该被添加或移除
.toggleClass( [switch ] )：一个用来判断样式类添加还是移除的 布尔值
.toggleClass( function(index, class, switch) [, switch ] )：用来返回在匹配的元素集合中的每个元素上用来切换的样式类名的一个函数。接收元素的索引位置和元素旧的样式类作为参数
注意事项：

toggleClass是一个互斥的逻辑，也就是通过判断对应的元素上是否存在指定的Class名，如果有就删除，如果没有就增加
toggleClass会保留原有的Class名后新增，通过空格隔开

```
//给所有的tr元素加一个class="c"的样式
$("#table tr").toggleClass("c");
//给所有的偶数tr元素切换class="c"的样式

//所有基数的样式保留，偶数的被删除
$("#table tr:odd").toggleClass("c");

//第二个参数判断样式类是否应该被添加或删除
//true，那么这个样式类将被添加;
//false，那么这个样式类将被移除
//所有的奇数tr元素，应该都保留class="c"样式
$("#table tr:even").toggleClass("c", true);
//这个操作没有变化，因为样式已经是存在的
```

### 样式操作

> 获取：

.css( propertyName ) ：获取匹配元素集合中的第一个元素的样式属性的计算值
.css( propertyNames )：传递一组数组，返回一个对象结果

> 设置：

 .css(propertyName, value )：设置CSS
.css( propertyName, function )：可以传入一个回调函数，返回取到对应的值进行处理
.css( properties )：可以传一个对象，同时设置多个样式


**通过.css()方法处理的是内联样式，直接通过元素的style属性附加到元素上的**

### 临时数据

jQuery的属性与样式之元素的数据存储
html5 dataset是新的HTML5标准，允许你在普通的元素标签里嵌入类似data-*的属性，来实现一些简单数据的存取。它的数量不受限制，并且也能由JavaScript动态修改，也支持CSS选择器进行样式设置。这使得data属性特别灵活，也非常强大。有了这样的属性我们能够更加有序直观的进行数据预设或存储。那么在不支持HTML5标准的浏览器中，我们如何实现数据存取?  jQuery就提供了一个.data()的方法来处理这个问题

使用jQuery初学者一般不是很关心data方式，这个方法是jquery内部预用的，可以用来做性能优化，比如sizzle选择中可以用来缓存部分结果集等等。当然这个也是非常重要的一个API了，常常用于我们存放临时的一些数据，因为它是直接跟DOM元素对象绑定在一起的

jQuery提供的存储接口
```
jQuery.data( element, key, value )   //静态接口,存数据
jQuery.data( element, key )  //静态接口,取数据   
.data( key, value ) //实例接口,存数据
.data( key ) //实例接口,存数据
```
2个方法在使用上存取都是同一个接口，传递元素，键值数据。在jQuery的官方文档中，建议用.data()方法来代替。

我们把DOM可以看作一个对象，那么我们往对象上是可以存在基本类型，引用类型的数据的，但是这里会引发一个问题，可能会存在循环引用的内存泄漏风险

通过jQuery提供的数据接口，就很好的处理了这个问题了，我们不需要关心它底层是如何实现，只需要按照对应的data方法使用就行了

同样的也提供2个对应的删除接口，使用上与data方法其实是一致的，只不过是一个是增加一个是删除罢了

jQuery.removeData( element [, name ] )
.removeData( [name ] )

```
//通过$.data方式设置数据
$.data($('.left'), "a", "data test")

//通过.data方式设置数据
var ele = $(this);
ele.data("a", "data test")；
ele.data("b", { name: "慕课网" })
```