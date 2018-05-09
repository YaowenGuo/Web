# 使用 html5 进行布局，划分内容

HTML5遵循语义和表现分离的哲学，而html负责语义化文档，为了让每个概念、观点或主题彼此分开，HTML5给出了几个新的语义标签，用于定义不同的区域。它们本身没有任何样式，因此很难看出应用和不用的区别。主要用来对结构进行处理，是语义和外观进行分离的基础工作。

元素       |  说明                      |  类型   |   新增或有无变化  
--------- | ------------------------- | ------- | -------------  
header    | 表示首部                   |   流     |  新增
section   | 表示一个重要的概念或主题      |   流     |  新增
footer    | 表示尾部                   |   流     |  新增
nav       | 表示有意集中在一起的导航      |   流     |  新增
aside     | 表示与主显示区域相关的内容稍有牵涉的内容 |  流      |  新增
h1 ~ h6   | 表示标题                   |   流     | 无变化
hgroup    | 将一组标题组织在一起，以便文档大纲只显示其中第一个标题 | 流   | 新增
article   | 表示一段独立内容            |   流     |  新增
address   | 表示文档或article的联系信息  |   流     |  新增
details   | 生成一个区域、用户将其展开可以获得更多细节内容 |  流  | 新增
summary   | 用在detail元素中，表示该元素的标题或说明 | 无 | 新增

从整体到具体的看整个元素是比较好的方式，一是人们的认识方式是从宏观到微观方式；另一个原因是，在编写真个web页面的时候，也是先从整个布局，然后到具体，一点一点实现的。

## header footer section 文档的结构划分

在构建一个页面时，最先做的就是对文档的结构进行划分，一般的页面都会有头、主题、页脚构成。HTML为了

### section 节，主题分块

section 表示文档中的一节，使用标题元素时，实际上也生成了隐含的节。使用section元素则可以明确地生成节并且将其与标题分开，至于什么时候应该使用section元素，并没有一个明确的规定。不过从经验上讲，section元素用来包含的是那种应该列入文档大纲或目录的内容。section元素通常包含一个或多个段落以及一个标题，不过标题不是必须的。

元素     | section
------- | ----
元素类型 | 流
父元素   | 任何可以包含流元素的元素。但section不能是address元素的后代元素。
局部属性 | 无
内容     | 流内容
标签用法  | 双标签
html新增  | 是
HTML5中变化 | 无
习惯样式   | section {display: block; }

```
<!DOCTYPE HTML>
<html>
    <head>
        <title>Example</title>
        <meta name="author" content="Adam Freeman"/>
        <meta name="description" content="A simple example"/>
        <link rel="shortcut icon" href="favicon.ico" type="image/x-icon" />
        <style>
            h1, h2, h3 { background: grey; color: white; }
            hgroup > h1 { margin-bottom: 0px; }
            hgroup > h2 { background: grey; color: white; font-size: 1em;
                         margin-top: 0px;}
        </style>
    </head>
    <body>
        <section>
            <hgroup>
                <h1>Fruits I Like</h1>
                <h2>How I Learned to Love Citrus</h2>
            </hgroup>
            I like apples and oranges.
            <section>
                <h1>Additional fruits</h1>
                I also like bananas, mangoes, cherries, apricots, plums,
                peaches and grapes.
                <section>            
                    <h1>More information</h1>
                    You can see other fruits I like <a href="fruitlist.html">here</a>.
                </section>
            </section>
        </section>

        <h1>Activities I like</h1>
        <p>I like to swim, cycle and run. I am in training for my first triathlon,
                    but it is hard work.</p>
        <h2>Kinds of Triathlon</h2>
        There are different kinds of triathlon - sprint, Olympic and so on.
        <h3>The kind of triathlon I am aiming for</h3>
        I am aiming for Olympic, which consists of the following:
        <ol>
            <li>1.5km swim</li>
            <li>40km cycle</li>
            <li>10km run</li>
        </ol>
    </body>
</html>
```

- 这个清单定义了三个嵌套的 section，而且每个 section 中的标题元素都是一个 h1，使用了 section 之后，浏览器就会理顺标题之间的层次关系，让作者从管理各个标题的正确次序中解脱出来——至少理论上是这样。然而实际上浏览器上会有出入。
- 不过仔细观察会发现，section 中的 h1 元素和 普通的同等级 hn 元素小。这是因为 Chrome、IE9在内的浏览器对位于 section、 article、 aside、和 nav员诉总的h1 元素应用的样式有所不同，他们给于这种样式下的 h1 元素与正常情况下下的 h2 元素相同。

### header footer 首部和尾部

header 表示一节的首部，并不是整个页面才有header。里面可以包含各种是和出现在首部的东西，包括刊头和徽标。在内嵌的元素方面，header 元素通常包含一个标题元素或一个 hgroup 元素，还可以包含该节的导航元素。

元素     | header
------- | ----
元素类型 | 流
父元素   | 任何可以包含流元素的元素。但不能是address、footer或其他header元素的后代元素。
局部属性 | 无
内容     | 流内容
标签用法  | 双标签
html新增  | 是
HTML5中变化 | 无
习惯样式   | header {display: block; }

footer 元素和header配套，表示一节的尾部，footer通常包含该节的总结信息，还可以包含作者的介绍，版权信息、到相关内容的连接、徽标、免责声明。

元素     | footer
------- | ----
元素类型 | 流
父元素   | 任何可以包含流元素的元素。但不能是address、header或其他footer元素的后代元素。
局部属性 | 无
内容     | 流内容
标签用法  | 双标签
html新增  | 是
HTML5中变化 | 无
习惯样式   | header {display: block; }


## h1 ~ h6 标题
hn 元素表示标题，HTML定义了从h1 ~ h6的一套标题体系，h1级别最高，依次减小。

元素     | h1 ~ h6
------- | ----
元素类型 | 流
父元素   | hgroup 元素或其他任何可以包含流元素的元素。这些元素不能是address元素的后代元素。
局部属性 | 无
内容     | style元素和流内容
标签用法  | 双标签
html新增  | 是
HTML5中变化 | 无
习惯样式   | section { display: block; }

h1 ~ h6 类似于章-节-文章-段之类的概念，用于将整个文档分成不同的部分，同一级的标题用于相同等级的部分。这些元素还有一个额外的好处是他们构成了文档的大纲，因此用户只要随便浏览一下文档的各级标题即可初步了解其大意和结构。我们通过标题体系还能迅速导航到感兴趣的内容。

虽然没有限制，但每个文档最好只有一个 h1 标题。大多数内容只会用到两到三级标题。除了合同和精确的技术文档，很少有什么内容有必要用到更深层次的标题。

各标题的习惯样式
元素  | 习惯样式
----- | -------
h1   | h1 { display: block; font-size: 2em; margin-before: 0.67em; margin-after: 0.67em; margin-start: 0; margin-end: 0; font-weight: bold; }
h2   | h2 { display: block; font-size: 1.5em; margin-before: 0.83em; margin-after: 0.83em;margin-start: 0; margin-end: 0; font-weight: bold; }
h3   | h3 { display: block; font-size: 1.17em; margin-before: 1em; margin-after: 1em; margin-start: 0; margin-end: 0; font-weight: bold; }
h4   | h4 { display: block; margin-before: 1.33em; margin-after: 1.33em; margin-start: 0; margin-end: 0; font-weight: bold; }
h5   | h5 { display: block; font-size: .83em; margin-before: 1.67em; margin-after: 1.67em; margin-start: 0; margin-end: 0; font-weight: bold; }
h6   | h6 { display: block; font-size: .67em; margin-before: 2.33em; margin-after: 2.33em; margin-start: 0; margin-end: 0; font-weight: bold; }


## hgroup (hidden group) 隐藏子标题

hgroup 将几个标题元素作为一个整体处理(想要使用标题，但是有不想其出现在目录结构中)，以免搅乱HTML文档的大纲

元素     | hgroup
------- | ----
元素类型 | 流
父元素   | 任何可以包含流元素的元素。
局部属性 | 无
内容     | 一个或多个标题元素(h1 ~ h6)
标签用法  | 双标签
html新增  | 是
HTML5中变化 | 无
习惯样式   | hgroup { display: block; }

hgroup 主要用来解决副标题问题，假设文档中有一段内容，其标题为“Fruits I Like”, 你可能还想给它起个副标题“How I Learned to Love Citrus”。但是当你使用h1、h2来标识这些标题时。
```
<h1>Fruits I Like</h1>
<h2>How I Learned to Love Citrus</h2>
I like apples and oranges.
<h2>Additional fruits</h2>
I also like bananas, mangoes, cherries,apricots, plums, peaches and grapes.
```
当生成各级标题的标签时，由于“How I Learned to Love Citrus”是和“Additional fruits”同一级的标签，会产生如下的标签结构

- Fruits I Like
  - How I Learned to Love Citrus
  - Additional fruits

然而“How I Learned to Love Citrus”只是一个副标题，我们并不想让它出现在标签结构中，此时就可以用到 `hgroup` 标签。
```
<hgroup>
	<h1>Fruits I Like</h1>
	<h2>How I Learned to Love Citrus</h2>
</hgroup>
I like apples and oranges.
<h2>Additional fruits</h2>
I also like bananas, mangoes, cherries,apricots, plums, peaches and grapes.
```

由于 `hgroup` 元素在 h1 ~ h6 标题体系中的位置取决于其字一个子标题元素，例如上述代码中，由于第一个标题元素是 `h1`，所以 `hgroup` 的元素级别相当于 h1 元素。所以只有 h1 标题会被列入文档的大纲。

- Fruits I Like
  - Additional fruits

这样副标题引起的混乱就被解决了，因为 hgroup 元素表明了它应该被忽略。
