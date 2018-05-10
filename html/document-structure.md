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


## nav 添加导航区域

nav 元素表示文档中的一个区域，它包含着到其他页面或统一页面的其他部分的连接。显然，并非所有的超链接都要放到 nav 元素中。该元素的目的是规划处文档的主要导航区域。
- 一个文档中可以有多个导航区域。
- 导航可以是指向文档外部导航（站内其它功能页面），也可以是文档内部不同区域的导航（标题导航)。
- 放在 header 中的导航调试它是主 nav，一般是关于真个页面或者整个站的。
- nav 元素可以包含任意任何流内容，而不仅限于超链接。

元素     | nav
------- | ----
元素类型 | 流
父元素   | 任何可以包含流元素的元素。但不能是address的后代。
局部属性 | 无
内容     | 流内容
标签用法  | 双标签
html新增  | 是
HTML5中变化 | 无
默认样式   | header {display: block; }

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


## artical 独立成篇的内容

artical 元素代表着 HTML 文档中一段独立成篇的内容，从理论上讲，可以独立于页面其余内容发布或使用。这不是说作者必须单独发布它，而是说判断是否使用该元素是要以独立性为依据。一篇新文章或博文条目都是这方面的典型例子。

元素     | article
------- | ----
元素类型 | 流
父元素   | 任何可以包含流元素的元素。但不能是address的后代。
局部属性 | 无
内容     | sytle元素和流内容
标签用法  | 双标签
html新增  | 是
HTML5中变化 | 无
默认样式   | header {display: block; }

- artical 甚至可以包含 header、footer、hgroup、h1 ~ h6、section 的内容。因为他们是一个整体的内容。
- artical 用法很灵活，甚至可以嵌套。例如博客的原文用一个，每次更新或得到的评论又用一个。与其他一些元素类似，artical元素与上下文相关。它可能在某种内容中能够带来富有含义的结构，而换个地方就未必如此。这需要文档作者自身衡量（并且保持用法的一致）。


## aside 生成附注栏

aside 用来表示跟周边内容稍微沾一点边的内容，类似于书籍或杂志中的侧栏。其内容与页面其他内容、article或section有点关系，但并非主体的一部分。它可能是一些背景信息、到相关文章的连接，诸如此类。

元素     | aside
------- | ----
元素类型 | 流
父元素   | 任何可以包含流元素的元素。但不能是address的后代。
局部属性 | 无
内容     | sytle元素和流内容
标签用法  | 双标签
html新增  | 是
HTML5中变化 | 无
默认样式   | header {display: block; }

aside 适合编写一些侧边栏等信息。

## address 提供联系信息

address 用来表示文档或article元素的联系信息。

元素     | address
------- | ----
元素类型 | 流
父元素   | 任何可以包含流元素的元素。
局部属性 | 无
内容     | 流内容。但标题元素h1 ~ h6、section、header、footer、nav、article和aside元素不能用作该元素的后代元素。
标签用法  | 双标签
html新增  | 是
HTML5中变化 | 无
默认样式   | address {display: block; font-style: italic; }

- address 作为 article 元素的后代时，它提供的联系信息被视为该 artical 的。否则，当 address 元素身为article 元素的后代时，它提供的联系信息被视为该artical的。当作为body 元素的子元素事（之间没有article元素），它提供的信息被视为整个文档的。
- address 元素不能用来表示文档或者和文章的联系信息之外的地址。例如，他不能用在文档中表示客户或用户的地址。

## details summary 生成详情信息

details 元素在文章中生成一个区域，用户可以展开它了解关于某主题的更多详情。这些都是浏览器自身就具有的。

元素     | details
------- | ----
元素类型 | 流
父元素   | 任何可以包含流元素的元素。
局部属性 | open
内容     | 流内容以及一个可有可无的summary元素。
标签用法  | 双标签
html新增  | 是
HTML5中变化 | 无
默认样式   | details {display: block; }

details 通常包含一个 summary 元素，后者的作用是为该详情区域生成一个说明标签或标题。

元素     | summary
------- | ----
元素类型 | 无
父元素   | details元素。
局部属性 | 无
内容     | 短语内容。
标签用法  | 双标签
html新增  | 是
HTML5中变化 | 无
默认样式   | summary {display: block; }
