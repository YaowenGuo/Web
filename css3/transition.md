# transition

过度是指，当一个动作（:hover, :focus, :active, :checked, 媒体查询、或者js改变了类和属性）触发某个样式改变时，不再像之前立即从原属性变为新的属性，而是在一定的时间区间内，从原有属性主键平滑地过度到新的属性值。

[TOC]

## transition 过渡

`transition: [<transition-property> || <transition-duration> || <transition-timing-function> || <transition-delay> ] [,* ]`

其中简写时，transition-duration 和 transition-delay 的顺序不能颠倒，因为这两个值都是实价。其他的次序无关紧要。
以上的四个选项可以作为四个单独的属性值来使用。

设置过渡的步骤

1. 在默认样式中声明元素的初始状样式
2. 声明过渡元素最终状态样式，比如悬浮状态
3. 在默认样式中添加过渡函数，添加一些不同的样式。

### transition-property 过渡的CSS属性

`transition-property: none | all | <single-transition-property> [',' <single-transitioin-property>] *`

可以使用逗号分隔对多个属性设置过渡。

- none: 不指定任何过渡
- all: 默认值，表示指定元素所有支持 transitin-property 属性的样式。
- <single-transition-property>: 指定CSS属性。需要注意，并不是所有属性都可以过渡，只有属性具有一个中点值的属性才能具备过渡效果。



### transition-duration 过渡时间

`transitioin-duration: <time>[, <time>]* ;`

当设置多个值时，transition-property 中的值按顺序与时间值逐一对应。也可以只设置一个值，会对所有属性应用同一过渡时间。

- time: 单位为 s 或 ms。


### transition-timing-function 缓动函数

此属性用于指定过渡变化的速度，可以说过预定义的函数，阶梯函数或者三次贝塞尔曲线。
`transitioin-timing-duration: <single-transition-timing-function> [, <single-transition-timing-function>]*;`

过渡函数也可以使用逗号分隔来指定多个，分别对应 transition-property 的属性值。

- 预定义的过渡函数
    - ease: 加速开始，减速结束
    - linear: 变化速度保持一致
    - ease-in: 加速开始
    - ease-out: 减速结束
    - ease-in-out: 加速开始，减速结束。跟 ease 有些不一样，要比 ease 加速的慢，减速的慢。
- 三次贝塞尔曲线 cubic-bezier(p1x, p1y, p2x, p2y);
    三次贝塞尔曲线有两个数据点和两个控制点。在 CSS 中起始点总是(0, 0),结束点总是(1, 1)。所以只剩下两个点，四个数值来控制贝塞尔曲线的变化。

- step(<integer> [, [start|end]]?) 函数用于把整个操作领域化成同样大小的间隔，每个间隔都是相等的。
    - integer: 用于指定 step 间隔的数量，大于 0 的正整数。
    - start, end: 可选参数，默认为 end。

### transition-delay 过渡开始出现的延迟时间

`transition-delay: <time> [,<time>]*;`

- 非负整数，延迟开始动画的时间。默认值为0。
- 负整数 元素会从触发点就开始，触发点之前的过渡动作会被截断。

```
a {
    color: red;
    transition: color 1s ease-in-out;
}
a: hover {
    color: blue;
}
```

## 过渡技巧

### 过渡结束事件

padding 动画结束触发的结束事件不统一，测试。

background-origin, web-kit IE 触发 background-origin-x 和 backgroound-origin-y


### 对 CSS 新加的属性的过渡有待测试。

例如 弹性布局的 order

过渡属性值是百分数是无法支持。尽管设置规范的一部分。
hover: 对宽度不能是用百分数，否则只能使用 hover 的结果作为实际宽度，不会改变。

image hover 不能触发尺寸改变！！！！

### 优先过渡的属性

当对一个输定定义了多次过渡时，大多数浏览器选择后一个作为要应用的变换。

### 多度开始或结束为 auto

大多不被过渡

### 隐式过渡

是指当一个属性过渡时，引起另一个属性过渡。多数浏览器支持隐式过渡，除了IE支持不够好。

### 用户体验

- 操作引起的过渡不宜过长。
- 过渡不易生硬

### 几乎无限延迟的过渡模拟 JS 操作

浏览器多过渡的时间并没有限制，可以使用段的激活过渡和很长的回归过渡，产生类似于 JS 改变了状态的错觉。

### 通过硬件加速使过渡更加流畅

有时，CSS 过渡动画并没有期待那样流畅，这通常是webkit 的问题。 可以通过设置 transform: translateZ(0); 来启动变换，此函数并不会改变元素，但是却开启了硬件加速。能够更好的起到平滑效果。
