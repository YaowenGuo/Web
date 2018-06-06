# animation

- animation 比 transition 声明更多的变化，animation 中可以应用 transition，形成多个有序的transition。
- animation 不需要触发动作也能够播放动画，而 transition必须有一个动作改变才成触发动画。



实现过程
1. 声明关键帧来声明一个动画
2. 在 animation 属性中调用关键帧声明的动画，从而实现一个更为复杂的动画效果。

## @keyframes 关键帧

我们看到的动画效果并不是连续的，而是一帧一帧的像似但变化有规律的图像快速播放形成的。由于视觉残留，在这些图像的切换速率达到一定数量时，人眼便无法分辨图像之间的差别，认为是连续的。而这些图像称为帧，在所有帧中，有一些帧的差别比较明显，这些帧可以变换为其他的帧，这些帧就是关键帧。

### 语法

keyframes 可以指定任何顺序来决定 animation 动画变化的关键位置。

`
@keyframes <ident> {
    from {
        /*CSS 样式*/
    }
    <percentage> {
        /*CSS 样式*/
    }

    to {
        /*CSS 样式*/
    }
}
`
- 格式为 @keyframes 开头， 加上一个标识名，后跟花括号。在花括号中写动画样式改变
- 一个 keyframe 由多个帧组成，这些帧使用 `百分比 {}` 构成，百分比表示在动画中的位置，花括号中写改位置时，元素具有的属性。浏览器会自动从一个帧平滑过渡到另一个帧。其中 百分比可以使用 ‘frome’ ‘to’ 表示 ‘0%’：开始，‘100%’结束。

- 百分比必须带 `%`， 即使是 `0%`
- keyframe 的语法规则还可以用如下的方式给出精确的定义
    - keyframes-rule: '@keyframe' IDENT '{' keyframe-blocks '}';
    - keyframes-blocks: [keyframe-selectors block] * ;
    - keyframe-selecters: ['frome' | 'to' PERCENTAGE] [',' ['frome' | 'to' PERCENTAGE]] * ;

```
@keyframes bounce {
    0%, 50%, 80%, 100% {
        transform: translateY(0);
    }
    40% {
        transform: translateY(-30px);
    }
    60% {
        transform: translateY(-15px);
    }
}


```

## animation 调用动画
直接在 css 选择器中使用 animation 属性调用 @keyframes 声明的动画。指定关键帧的名字和执行的时间。

animation 同样是一个复合属性，它包含了众多子属性。

`animation: [<animation-name> || <animation-duration> || <animation-timing-function> || <animation-delay> || <animation-iteration-count> || <animation-direction> || <animation-play-state> || <animation-fill-mode>] *`

### animation-name

主要用来指定一个关键帧声明好的动画的名字，这个动画名必须对应一个 @keyframes 规则。CSS 加载时会应用 animation-name 指定的动画，从而执行动画。

animation-name: none | IDENT [, none | IDENT]* ;

- none: 没有动画。

### animation-duration 动画播放时间

动画播放时间可以以秒，毫秒为单位。

animation-duration: <time> [,<time>]* ;


### animation-timing-function 播放方式

与 transition-timing-function 可接受的值一样。

### animation-delay 延迟

动画开始时间。

### animation-iteration-count 动画播放循环次数

animation-iteration-count: infinite | <number> [, infinite | <number>]* ;
- infinite: 无限循环播放
- number: 自然数，默认值是1。


### animation-direction 动画播放方向

设置循环播放时，某次的播放方向。

animation-direction: normal | alternate [, normal | alternate] *

- noraml: 每次都向前播放。默认自
- alternate: 偶数次循环向前播放，奇数次循环倒叙播放。


### animation-play-state 控制动画播放状态

animation-play-state: running | paused [, running | paused] *

- running: 正常播放，可以应用 running 将暂停的动画重新播放
- paused: 将正在进行的动画暂停下来，如果暂停了动画的播放，元素的样式将回到最原始的设置状态。

### animation-fill-mode 设置动画时间外属性

用户设置在动画开始前和结束后发生的动作。

animation-fill-mode: none | forwards | backwords | both

- none: 默认值，表示动画完成时，动画会翻转到初始帧处。
- forwards: 动画完成后会继续应用最后帧。
- backwords: 元素应用动画样式时循序应用动画的初始帧。
- both: 同时具有 forward 和 backward 的效果。

默认情况下，动画不会影响他的关键帧之外的属性，但使用 animation-full-mode 属性，可以修改动画的默认行为。可以让元素在动画结束后停留在一个关键帧上。
