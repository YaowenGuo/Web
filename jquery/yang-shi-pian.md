## jQuery对象与DOM对象
对于才开始接触jQuery库的初学者，我们需要清楚认识一点：

> jQuery对象与DOM对象是不一样的

可能一时半会分不清楚哪些是jQuery对象，哪些是DOM对象，下面重点介绍一下jQuery对象，以及两者相互间的转换。

通过一个简单的例子，简单区分下jQuery对象与DOM对象：
```
<p id=”imooc”></p>
```
我们要获取页面上这个id为imooc的p元素，然后给这个文本节点增加一段文字：“Hello Wrod!”，并且让文字颜色变成红色。

普通处理，通过标准JavaScript处理：
```
var p = document.getElementById('imooc');
p.innerHTML = 'Hello Wrod!';
p.style.color = 'red';
```
通过原生DOM模型提供的document.getElementById(“imooc”) 方法获取的DOM元素就是一个DOM对象，再通过innerHTML与style属性处理文本与颜色。

jQuery的处理：
```
var $p = $('#imooc');
$p.html('Hello Wrod!').css('color','red');
```
通过$('#imooc')方法会得到一个$p的jQuery对象，$p是一个类数组对象。这个对象里面包含了DOM对象的信息，然后封装了很多操作方法，调用自己的方法html与css，得到的效果与标准的JavaScript处理结果是一致的。

通过标准的JavaScript操作DOM与jQuyer操作DOM的对比，我们不难发现：

通过jQuery方法包装后的对象，是一个类数组对象。它与DOM对象完全不同，唯一相似的是它们都能操作DOM。
通过jQuery处理DOM的操作，可以让开发者更专注业务逻辑的开发，而不需要我们具体知道哪个DOM节点有那些方法，也不需要关心不同浏览器的兼容性问题，我们通过jQuery提供的API进行开发，代码也会更加精短。
PS：大家这里做个大概印象就OK，后面会有深入的讲解。

```
<!DOCTYPE html>
<html>

<head>
    <meta http-equiv="Content-type" content="text/html; charset=utf-8" />
    <title></title>
    <script src="http://code.jquery.com/jquery-1.11.3.js"></script>
    
    <!-- 使用JS原生语法 -->
    <script type="text/javascript">
        window.onload = function(){
            // 通过原生JS语法获取id为imooc1的元素p
			var p = document.getElementById('imooc1');
            // 将元素p在html中内容改变
			p.innerHTML = 'P1：您好！通过慕课网学习jQuery才是最佳的途径';
            // 将元素p的内容颜色改为红色
			p.style.color = 'red';	
    	}
    </script>
    
    <!-- 使用jQuery语法 -->
    <script type="text/javascript">
        $(document).ready(function() {
            /**
             * 通过jQuery语法获取id为imooc2的元素获得一个jQuery对象
             * 调用该对象的html()方法进行更改内容
             * 调用该对象的css()方法进行更改颜色样式
             */   
            var $p = $('#imooc2');
            $p.html('P2：您好！通过慕课网学习jQuery才是最佳的途径').css('color','red');
        });
    </script>
    
</head>

<body>
    <p id="imooc1"></p>
    <p id="imooc2"></p>
</body>

</html>
```

## jQuery对象转化成DOM对象
    jQuery库本质上还是JavaScript代码，它只是对JavaScript语言进行包装处理，为的是提供更好更方便快捷的DOM处理与开发中经常使用的功能。我们使用jQuery的同时也能混合JavaScript原生代码一起使用。在很多场景中，我们需要jQuery与DOM能够相互的转换，它们都是可以操作的DOM元素，jQuery是一个类数组对象，而DOM对象就是一个单独的DOM元素。

如何把jQuery对象转成DOM对象？

利用数组下标的方式读取到jQuery中的DOM对象

HTML代码
```
<div>元素一</div>
<div>元素二</div>
<div>元素三</div>
```
JavaScript代码
```
var $div = $('div') //jQuery对象
var div = $div[0] //转化成DOM对象
div.style.color = 'red' //操作dom对象的属性
```
用jQuery找到所有的div元素（3个），因为jQuery对象也是一个数组结构，可以通过数组下标索引找到第一个div元素，通过返回的div对象，调用它的style属性修改第一个div元素的颜色。这里需要注意的一点是，数组的索引是从0开始的，也就是第一个元素下标是0

通过jQuery自带的get()方法

jQuery对象自身提供一个.get() 方法允许我们直接访问jQuery对象中相关的DOM节点，get方法中提供一个元素的索引：
```
var $div = $('div') //jQuery对象
var div = $div.get(0) //通过get方法，转化成DOM对象
div.style.color = 'red' //操作dom对象的属性
```
其实我们翻开源码，看看就知道了，get方法就是利用的第一种方式处理的，只是包装成一个get让开发者更直接方便的使用。

## DOM对象转化成jQuery对象
相比较jQuery转化成DOM，开发中更多的情况是把一个dom对象加工成jQuery对象。$(参数)是一个多功能的方法，通过传递不同的参数而产生不同的作用。

如果传递给$(DOM)函数的参数是一个DOM对象，jQuery方法会把这个DOM对象给包装成一个新的jQuery对象
通过$(dom)方法将普通的dom对象加工成jQuery对象之后，我们就可以调用jQuery的方法了

HTML代码
```
<div>元素一</div>
<div>元素二</div>
<div>元素三</div>
```
JavaScript代码
```
var div = document.getElementsByTagName('div'); //dom对象
var $div = $(div); //jQuery对象
var $first = $div.first(); //找到第一个div元素
$first.css('color', 'red'); //给第一个元素设置颜色
```
通过getElementsByTagName获取到所有div节点的元素，结果是一个dom合集对象，


### jQuery选择器之id选择器
页面的任何操作都需要节点的支撑，开发者如何快速高效的找到指定的节点也是前端开发中的一个重点。jQuery提供了一系列的选择器帮助开发者达到这一目的，让开发者可以更少的处理复杂选择过程与性能优化，更多专注业务逻辑的编写。

jQuery几乎支持主流的css1~css3选择器的写法，我们从最简单的也是最常用的开始学起

id选择器：一个用来查找的ID，即元素的id属性

$( "#id" )
id选择器也是基本的选择器，jQuery内部使用JavaScript函数document.getElementById()来处理ID的获取。原生语法的支持总是非常高效的，所以在操作DOM的获取上，如果能采用id的话尽然考虑用这个选择器

值得注意：

id是唯一的，每个id值在一个页面中只能使用一次。如果多个元素分配了相同的id，将只匹配该id选择集合的第一个DOM元素。但这种行为不应该发生;有超过一个元素的页面使用相同的id是无效的

### jQuery选择器之类选择器
类选择器，顾名思义，通过class样式类名来获取节点

描述：

$( ".class" )
类选择器，相对id选择器来说，效率相对会低一点，但是优势就是可以多选

同样的jQuery在实现上，对于类选择器，如果浏览器支持，jQuery使用JavaScript的原生getElementsByClassName()函数来实现的

下边实现一个原生getElementsByClassName()函数的实现代码与jQuery实现代码的比较
```
//通过原生方法处理
//样式是可以多选的，所以得到的是一个合集
//需要通过循环给合集中每一个元素修改样式
var divs = document.getElementsByClassName('aaron');
for (var i = 0; i < divs.length; i++) {
    divs[i].style.border = "3px solid blue";
}

//通过jQuery直接传入class
//class选择器可以选择多个元素
$(".aaron").css("border", "3px solid red");
```
      
我们不难发现：jQuery除了选择上的简单，而且没有再次使用循环处理
不难想到$(".imooc").css()方法内部肯定是带了一个隐式的循环处理，所以使用jQuery选择节点，不仅仅只是选择上的简单，同时还增加很多关联的便利操作，后续我们还会慢慢的学到其他的优势。


不过这个对象是一个数组合集(3个div元素)。通过$(div)方法转化成jQuery对象，通过调用jQuery对象中的first与css方法查找第一个元素并且改变其颜色。

### jQuery选择器之元素选择器
元素选择器：根据给定（html）标记名称选择所有的元素

描述：

$( "element" )
搜索指定元素标签名的所有节点，这个是一个合集的操作。同样的也有原生方法getElementsByTagName()函数支持

右边编辑器代码所示：

第一组：通过getElementsByTagName方法得到页面所有的<div>元素

var divs = document.getElementsByTagName('div');
divs是dom合集对象，通过循环给每一个合集中的<div>元素赋予新的border样式

第二组：同样的效果，$("p")选取所有的<p>元素，通过css方法直接赋予样式

### jQuery选择器之元素选择器
元素选择器：根据给定（html）标记名称选择所有的元素

描述：

$( "element" )
搜索指定元素标签名的所有节点，这个是一个合集的操作。同样的也有原生方法getElementsByTagName()函数支持

右边编辑器代码所示：
```
//通过原生方法处理
//获取到所有的节点标记名为div的元素
//给每一个div加上蓝色的边框

var divs = document.getElementsByTagName('div');
for (var i = 0; i < divs.length; i++) {
    divs[i].style.border = "3px solid blue";
}

//通过jQuery直接传入标签名p
//标签是可以多个的，所以得到的同样也是一个合集
$("p").css("border", "3px solid red");
```  

通过getElementsByTagName方法得到页面所有的<div>元素

var divs = document.getElementsByTagName('div');
divs是dom合集对象，通过循环给每一个合集中的<div>元素赋予新的border样式

同样的效果，$("p")选取所有的<p>元素，通过css方法直接赋予样式

### jQuery选择器之全选择器（*选择器）
在CSS中，经常会在第一行写下这样一段样式

* {padding: 0; margin: 0;}
通配符*意味着给所有的元素设置默认的边距。jQuery中我们也可以通过传递*选择器来选中文档页面中的元素

描述：

$( "*" )
抛开jQuery，如果要获取文档中所有的元素，通过document.getElementsByTagName()中传递"*"同样可以获取到

不难发现，id、class、tag都可以通过原生的方法获取到对应的节点，但是我们还需要考虑一个兼容性的问题，我这里顺便提及一下，比如:

IE会将注释节点实现为元素，所以在IE中调用getElementsByTagName里面会包含注释节点，这个通常是不应该的
getElementById的参数在IE8及较低的版本不区分大小写
IE7及较低的版本中，表单元素中，如果表单A的name属性名用了另一个元素B的ID名并且A在B之前，那么getElementById会选中A
IE8及较低的版本，浏览器不支持getElementsByClassName
看到了吧，作为一名合格的前端不是那么简单的，就一个基本的选择器上面都需要做这么多兼容，幸好有jQuery的出现，让我们省了很多功夫，如果大家对jQuery的实现感兴趣，可以看我另一个门课程 《jQuery源码解析》

### jQuery选择器之层级选择器
文档中的所有的节点之间都是有这样或者那样的关系。我们可以把节点之间的关系可以用传统的家族关系来描述，可以把文档树当作一个家谱，那么节点与节点直接就会存在父子，兄弟，祖孙的关系了。

选择器中的层级选择器就是用来处理这种关系

> 子元素 后代元素 兄弟元素 相邻元素

通过一个列表，对比层级选择器的区别

![](/assets/5590e98b0001f60d06130229.jpg)

 仔细观察层级选择器之间还是有很多相似与不同点

层级选择器都有一个参考节点
后代选择器包含子选择器的选择的内容
一般兄弟选择器包含相邻兄弟选择的内容
相邻兄弟选择器和一般兄弟选择器所选择到的元素，必须在同一个父元素下
```
<!DOCTYPE html>
<html>

<head>
    <meta http-equiv="Content-type" content="text/html; charset=utf-8" />
    <title></title>
    <link rel="stylesheet" href="imooc.css" type="text/css">
    <script src="https://www.imooc.com/static/lib/jquery/1.9.1/jquery.js"></script>
</head>

<body>
    <h2>子选择器与后代选择器</h2>
    <div class="left">
        <div class="aaron">
            <p>div下的第一个p元素</p>
        </div>
        <div class="aaron">
            <p>div下的第一个p元素</p>
        </div>
    </div>
    <div class="right">
        <div class="imooc">
            <article>
                <p>div下的article下的p元素</p>
            </article>
        </div>
        <div class="imooc">
            <article>
                <p>div下的article下的p元素</p>
            </article>
        </div>
    </div>

    <script type="text/javascript">
        //子选择器
        //$('div > p') 选择所有div元素里面的子元素P
        $('div > p').css("border", "1px groove red");
    </script>

    <script type="text/javascript">
        //后代选择器
        //$('div  p') 选择所有div元素里面的p元素
        $('div p').css("border", "1px groove red");
    </script>


    <h2>相邻兄弟选择器与一般兄弟选择器</h2>
    <div class="bottom">
        <div>兄弟节点div, +~选择器不能向前选择</div>
        <span class="prev">选择器span元素</span>
        <div>span后第一个兄弟节点div</div>
        <div>兄弟节点div
            <div class="small">子元素div</div>
        </div>
        <span>兄弟节点span,不可选</span>
        <div>兄弟节点div</div>
    </div>

    <script type="text/javascript">
        //相邻兄弟选择器
        //选取prev后面的第一个的div兄弟节点
        $(".prev + div").css("border", "3px groove blue");
    </script>

    <script type="text/javascript">
        //一般相邻选择器
        //选取prev后面的所有的div兄弟节点
        $(".prev ~ div").css("border", "3px groove blue");
    </script>

</body>

</html>
```

### jQuery选择器之基本筛选选择器
很多时候我们不能直接通过基本选择器与层级选择器找到我们想要的元素，为此jQuery提供了一系列的筛选选择器用来更快捷的找到所需的DOM元素。筛选选择器很多都不是CSS的规范，而是jQuery自己为了开发者的便利延展出来的选择器

筛选选择器的用法与CSS中的伪元素相似，选择器用冒号“：”开头，通过一个列表，看看基本筛选器的描述：

![](/assets/筛选选择器.jpg)

注意事项：

:eq(), :lt(), :gt(), :even, :odd 用来筛选他们前面的匹配表达式的集合元素，根据之前匹配的元素在进一步筛选，注意jQuery合集都是从0开始索引
gt是一个段落筛选，从指定索引的下一个开始，gt(1) 实际从2开始

```
<!DOCTYPE html>
<html>

<head>
    <meta http-equiv="Content-type" content="text/html; charset=utf-8" />
    <title></title>
    <link rel="stylesheet" href="imooc.css" type="text/css">
    <script src="https://www.imooc.com/static/lib/jquery/1.9.1/jquery.js"></script>
</head>

<body>
    <h2>基本筛选器</h2>
    <h3>:first/:last/:even/:odd</h3>
    <div class="left">
        <div class="div">
            <p>div:first</p>
            <p>:even</p>
        </div>
        <div class="div">
            <p>:odd</p>
        </div>
        <div class="div">
            <p>:even</p>
        </div>
        <div class="div">
            <p>:odd</p>
        </div>
        <div class="div">
            <p>:even</p>
        </div>
        <div class="div">
            <p>div:last</p>
            <p>:odd</p>
        </div>
    </div>
    <script type="text/javascript">
    //找到第一个div
    $(".div:first").css("color", "#CD00CD");
    </script>
    
    <script type="text/javascript">
    //找到最后一个div
    $(".div:last").css("color", "#CD00CD");
    </script>
    
    <script type="text/javascript">
    //:even 选择所引值为偶数的元素，从 0 开始计数
    $(".div:even").css("border", "3px groove red");
    </script>
    
    <script type="text/javascript">
    //:odd 选择所引值为奇数的元素，从 0 开始计数
    $(".div:odd").css("border", "3px groove blue");
    </script>
    
    
    <h3>:eq/:gt/:lt</h3>
    <div class="left">
        <div class="aaron">
            <p>:lt(3)</p>
        </div>
        <div class="aaron">
            <p>:lt(3)</p>
        </div>
        <div class="aaron">
            <p>:eq(2)</p>
        </div>
        <div class="aaron">
        </div>
        <div class="aaron">
            <p>:gt(3)</p>
        </div>
        <div class="aaron">
            <p>:gt(3)</p>
        </div>
    </div>
    <script type="text/javascript">
    //:eq
    //选择单个
    $(".aaron:eq(2)").css("border", "3px groove blue");
    </script>
    
    <script type="text/javascript">
    //:gt 选择匹配集合中所有索引值大于给定index参数的元素
    $(".aaron:gt(3)").css("border", "3px groove blue");
    </script>
    
     <script type="text/javascript">
    //:lt 选择匹配集合中所有索引值小于给定index参数的元素
    //与:gt相反
    $(".aaron:lt(2)").css("color", "#CD00CD");
    </script>
    
    <h3>:not</h3>
    <div class="left">
        <div>
            <input type="checkbox" name="a" />
            <p>Aaron</p>
        </div>
        <div>
            <input type="checkbox" name="b" />
            <p>慕课</p>
        </div>
        <div>
            <input type="checkbox" name="c" checked="checked" />
            <p>其他</p>
        </div>
    </div>
    <script type="text/javascript">
        //:not 选择所有元素去除不匹配给定的选择器的元素
        //选中所有紧接着没有checked属性的input元素后的p元素，赋予颜色
        $("input:not(:checked) + p").css("background-color", "#CD00CD");
    </script>
</body>

</html>
```

### jQuery选择器之内容筛选选择器
基本筛选选择器针对的都是元素DOM节点，如果我们要通过内容来过滤，jQuery也提供了一组内容筛选选择器，当然其规则也会体现在它所包含的子元素或者文本内容上

内容过滤器描述如下表：

![](/assets/内容筛选选择器.jpg)

注意事项：

:contains与:has都有查找的意思，但是contains查找包含“指定文本”的元素，has查找包含“指定元素”的元素
如果:contains匹配的文本包含在元素的子元素中，同样认为是符合条件的。
:parent与:empty是相反的，两者所涉及的子元素，包括文本节点

```
<!DOCTYPE html>
<html>

<head>
    <meta http-equiv="Content-type" content="text/html; charset=utf-8" />
    <title></title>
    <link rel="stylesheet" href="imooc.css" type="text/css">
    <script src="https://www.imooc.com/static/lib/jquery/1.9.1/jquery.js"></script>
</head>

<body>
    <h2>内容筛选器</h2>
    <h3>:contains/:has</h3>
    <div class="left">
        <div class="div">
            <p>:contains go on</p>
        </div>
        <div class="div">
            <p>:contains</p>
        </div>
        <div class="div">
            <p>
                <span>:has</span>
            </p>
        </div>
        <div class="div">
            <p>:contains</p>
        </div>
    </div>

    <script type="text/javascript">
        //查找所有class='div'中DOM元素中包含"contains"的元素节点
        //并且设置颜色
        $(".div:contains(':contains')").css("color", "#CD00CD");
    </script>

    <script type="text/javascript">
        //查找所有class='div'中DOM元素中包含"span"的元素节点
        //并且设置颜色
        $(".div:has(span)").css("color", "blue");
    </script>


    <h3>:parent/:empty</h3>
    <div class="left">
        <div class="aaron">
            <a>:parent</a>
        </div>
        <div class="aaron">
            <a>:parent</a>
        </div>
        <div class="aaron">
            <a>:parent</a>
        </div>
        <div class="aaron">
            <a></a>
        </div>
    </div>
    <script type="text/javascript">
       //选择所有包含子元素或者文本的a元素
       //增加一个蓝色的边框
       $("a:parent").css("border", "3px groove blue");
    </script>

    <script type="text/javascript">
       //找到a元素下面的所有空节点(没有子元素)
       //增加一段文本与边框
       $("a:empty").text(":empty").css("border", "3px groove red"); 
    </script>

</body>

</html>
```

### 可见性筛选选择器
元素有显示状态与隐藏状态，jQuery根据元素的状态扩展了可见性筛选选择器:visible与:hidden

描述如下：

![](/assets/可见性筛选选择器.jpg)

这2个选择器都是 jQuery 延伸出来的，看起来比较简单，但是元素可见性依赖于适用的样式

:hidden选择器，不仅仅包含样式是display="none"的元素，还包括隐藏表单、visibility等等
我们有几种方式可以隐藏一个元素：

CSS display的值是none。
type="hidden"的表单元素。
宽度和高度都显式设置为0。
一个祖先元素是隐藏的，该元素是不会在页面上显示
CSS visibility的值是hidden
CSS opacity的指是0
如果元素中占据文档中一定的空间,元素被认为是可见的。
可见元素的宽度或高度，是大于零。
元素的visibility: hidden 或 opacity: 0被认为是可见的，因为他们仍然占用空间布局。
不在文档中的元素是被认为是不可见的，如果当他们被插入到文档中，jQuery没有办法知道他们是否是可见的，因为元素可见性依赖于适用的样式

### 属性筛选选择器
属性选择器让你可以基于属性来定位一个元素。可以只指定该元素的某个属性，这样所有使用该属性而不管它的值，这个元素都将被定位，也可以更加明确并定位在这些属性上使用特定值的元素，这就是属性选择器展示它们的威力的地方。

描述如下：

![](/assets/属性筛选选择器.jpg)

浏览器支持：

[att=val]、[att]、[att|=val]、[att~=val]  属于CSS 2.1规范
[ns|attr]、[att^=val]、[att*=val]、[att$=val] 属于CSS3规范
[name!="value"]  属于jQuery 扩展的选择器
CSS选择器无论CSS2.1版本还是CSS3版本，IE7和IE8都支持，webkit、Gecko核心及Opera也都支持，只有IE6以下浏览器才不支持
在这么多属性选择器中[attr="value"]和[attr*="value"]是最实用的

[attr="value"]能帮我们定位不同类型的元素，特别是表单form元素的操作，比如说input[type="text"],input[type="checkbox"]等
[attr*="value"]能在网站中帮助我们匹配不同类型的文件

```html
<!DOCTYPE html>
<html>

<head>
    <meta http-equiv="Content-type" content="text/html; charset=utf-8" />
    <title></title>
    <link rel="stylesheet" href="imooc.css" type="text/css">
    <script src="https://www.imooc.com/static/lib/jquery/1.9.1/jquery.js"></script>
</head>

<body>
    <h2>属性筛选选择器</h2>
    <h3>[att=val]、[att]、[att|=val]、[att~=val]</h3>
    <div class="left" testattr="true" >
        <div class="div" testattr="true" name='p1'>
            <a>[att=val]</a>
        </div>
        <div class="div" testattr="true" p2>
            <a>[att]</a>
        </div>
        <div class="div" testattr="true" name="-">
            <a>[att|=val]</a>
        </div>
        <div class="div" testattr="true" name="a b">
            <a>[att~=val]</a>
        </div>
    </div>

    <script type="text/javascript">
         //查找所有div中，属性name=p1的div元素
         $('div[name=p1]').css("border", "3px groove red"); 
    </script>

    <script type="text/javascript">
        //查找所有div中，有属性p2的div元素
        $('div[p2]').css("border", "3px groove blue"); 
    </script>

    <script type="text/javascript">
        //查找所有div中，有属性name中的值只包含一个连字符“-”的div元素
        $('div[name|="-"]').css("border", "3px groove #00FF00"); 
    </script>

    <script type="text/javascript">
        //查找所有div中，有属性name中的值包含一个连字符“空”和“a”的div元素
        $('div[name~="a"]').css("border", "3px groove #668B8B"); 
    </script>


    <h3>[att^=val]、[att*=val]、[att$=val]、[att!=val]</h3>
    <div class="left" testattr="true" >
        <div class="div" testattr="true"  name='imooc-aaorn'>
            <a>[att^=val]</a>
        </div>
        <div class="div" testattr="true"  name='aaorn-imooc'>
            <a>[att$=val]</a>
        </div>
        <div class="div" testattr="true"  name="attr-test-selector">
            <a>[att*=val]</a>
        </div>
        <div class="div" name="a b">
            <a>[att!=val]</a>
        </div>
    </div>


    <script type="text/javascript">
         //查找所有div中，属性name的值是用imooc开头的
         $('div[name^=imooc]').css("border", "3px groove red"); 
    </script>

    <script type="text/javascript">
         //查找所有div中，属性name的值是用imooc结尾的
         $('div[name$=imooc]').css("border", "3px groove blue"); 
    </script>

    <script type="text/javascript">
        //查找所有div中，有属性name中的值包含一个test字符串的div元素
        $('div[name*="test"]').css("border", "3px groove #00FF00"); 
    </script>

    <script type="text/javascript">
        //查找所有div中，有属性testattr中的值没有包含"true"的div
        $('div[testattr!="true"]').css("border", "3px groove #668B8B"); 
    </script>


</body>

</html>
```
### 子元素筛选选择器

子元素筛选选择器不常使用，其筛选规则比起其它的选择器稍微要复杂点

子元素筛选选择器描述表：



注意事项：

1. :first只匹配一个单独的元素，但是:first-child选择器可以匹配多个：即为每个父级元素匹配第一个子元素。这相当于:nth-child(1)
2. :last 只匹配一个单独的元素， :last-child 选择器可以匹配多个元素：即，为每个父级元素匹配最后一个子元素
3. 如果子元素只有一个的话，:first-child与:last-child是同一个
4. :only-child匹配某个元素是父元素中唯一的子元素，就是说当前子元素是父元素中唯一的元素，则匹配
5. jQuery实现:nth-child(n)是严格来自CSS规范，所以n值是“索引”，也就是说，从1开始计数，:nth-child(index)从1开始的，而eq(index)是从0开始的
6. nth-child(n) 与 :nth-last-child(n) 的区别前者是从前往后计算，后者从后往前计算


### 表单元素选择器
无论是提交还是传递数据，表单元素在动态交互页面的作用是非常重要的。jQuery中专门加入了表单选择器，从而能够极其方便地获取到某个类型的表单元素

表单选择器的具体方法描述：

![](/assets/表单元素选择器.jpg)

注意事项：

除了input筛选选择器，几乎每个表单类别筛选器都对应一个input元素的type值。大部分表单类别筛选器可

### 表单对象属性筛选选择器
除了表单元素选择器外，表单对象属性筛选选择器也是专门针对表单元素的选择器，可以附加在其他选择器的后面，主要功能是对所选择的表单元素进行筛选

表单筛选选择器的描述：

![](/assets/表单对象属性筛选选择器.jpg)

注意事项：

选择器适用于复选框和单选框，对于下拉框元素, 使用 :selected 选择器
在某些浏览器中，选择器:checked可能会错误选取到<option>元素，所以保险起见换用选择器input:checked，确保只会选取<input>元素

### 特殊选择器this
相信很多刚接触jQuery的人，很多都会对$(this)和this的区别模糊不清，那么这两者有什么区别呢？

this是JavaScript中的关键字，指的是当前的上下文对象，简单的说就是方法/属性的所有者

下面例子中，imooc是一个对象，拥有name属性与getName方法,在getName中this指向了所属的对象imooc

var imooc = {
    name:"慕课网",
    getName:function(){
        //this,就是imooc对象
        return this.name;
    }
}
imooc.getName(); //慕课网
当然在JavaScript中this是动态的，也就是说这个上下文对象都是可以被动态改变的(可以通过call,apply等方法)，具体的大家可以查阅相关资料

同样的在DOM中this就是指向了这个html元素对象，因为this就是DOM元素本身的一个引用

假如给页面一个P元素绑定一个事件:
```
p.addEventListener('click',function(){
    //this === p
    //以下两者的修改都是等价的
    this.style.color = "red";
    p.style.color = "red";
},false);
```
通过addEventListener绑定的事件回调中，this指向的是当前的dom对象，所以再次修改这样对象的样式，只需要通过this获取到引用即可

 this.style.color = "red"
但是这样的操作其实还是很不方便的，这里面就要涉及一大堆的样式兼容，如果通过jQuery处理就会简单多了，我们只需要把this加工成jQuery对象

换成jQuery的做法：
```
$('p').click(function(){
    //把p元素转化成jQuery的对象
    var $this= $(this) 
    $this.css('color','red')
})
```
通过把$()方法传入当前的元素对象的引用this，把这个this加工成jQuery对象，我们就可以用jQuery提供的快捷方法直接处理样式了

总体：

this，表示当前的上下文对象是一个html对象，可以调用html对象所拥有的属性和方法。
$(this),代表的上下文对象是一个jquery的上下文对象，可以调用jQuery的方法和属性值。

