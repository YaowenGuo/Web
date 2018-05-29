# border

## border 边框

border 在之前的版中就存在了，它是一个复合属性，可以分开使用。

border: border-width border-style border-color;

所写的属性以空格分割，并且它们没有顺序，唯一必要的值是border-style，否则没有效果，其他值可以省略。
- border-width: 默认值为 menium（大约在3~4px）
- border-color: 默认值是字体的颜色
- border-sytle: 默认值为none，省略将不显示。
    - none: 无边框
    - hidden: 不显示
    - dotted: 点状边框
    - dashed: 虚线
    - solid: 实线
    - double: 双线
    - groove: 定义3D凹槽边框
    - ridge: 定义3D垄状边框
    - inset: 3D inset边框
    - ourset: 3D outset边框
    - inherit: 继承父元素类型

border属性村从TLBL原则（Top、Right、Bottom、Left），可以单独设置某边。

分开写是，可以设置多边一起设置不同的属性。

> 以下为CSS3新增的下过

## border-color 《还未支持》多种颜色边框

border-<borter>-color: [<color> | transparent]{1, 4} | inherit;

为了避免和CSS2冲突，CSS3中的多颜色不再支持简写形式，必须指定具体边。

## border-image 边框图

border-image: none | <border-image-source> <border-image-slice>  <border-image-width> ? <border-image-repeat>;

### border-image-source 图片源

border-image-source: url(img_url);

### border-image-slice 切割

border-image-slice: [<number> | <percentage>] {1, 4} && fill ?;

- number: 用于从边缘切割掉的的宽度，没有单位，默认就是像素，可以使用1 ~ 4 个值，和border-width含义一样。
- percentage: 使用百分比表示从各边向内切割掉的宽度，可以使用1 ~ 4 个值。

- fill: 如果使用该关键字，图片中间的部分将保留下来，默认情况为空。

切割其实是以九宫格的形式将图片切成了9部分，以每一小块来重复或者拉伸。


### border-image-width 宽度

border-image-width: [<number> | <percentage>] {1, 4};

虽然规定了改属性，但是还以以border-width为准。

- number: 用于设置边框图片大小的像素值，可以使用1 ~ 4 个值，和border-width含义一样。
- percentage: 使用百分比设置边框图片大小，可以使用1 ~ 4 个值。

### border-image-repeat 显示方法

border-image-repeat: [stretch | repeat | round] {0, 2};

border-image-repeat只能对边一样活着四边一样这是。

### border-image-outset

## border-radius 圆角

border-radius: none | <length>{1, 4} | [/<length>{1, 4}]?;

- length可以使用像素或百分数。
- 该属性也是一个复合属性，能够制定1 ~ 4 值制定不同给的边。
- 如果斜线存在，则前面的值是水平方向上的半径，斜线后面的值是指定垂直方向上的半径。以此可以设置椭圆角。
- 应用于表格时，只有 border-collapse 为 separate 时才能正常显示圆角。

另外他们还可以分开指定

border-top-left-radius
border-top-right-radius
border-botton-right-radius
border-botton-left-radius

圆角其实是border的外边角，当 border 很大时，内角并不会被切掉。这是因为，border-redius 指定的是外边半径，而内边半径等于外边半径减去边框厚度。如果该差值小于等于0，那内角将是直角。差值越大，内角半径越大。

## box-shadow 阴影

box-shadow: none | [inset x-offset y-offset blur-radius spread-radius color ], [inset x-offset y-offset blur-radius spread-radius color ]

- none: 默认值，没有阴影效果
- inset: 阴影类型，可选值。默认是外阴影。如果这是了inset，则为内阴影。
- x-offset: 阴影水平偏移量，正值阴影在右侧
- y-offset: 阴影垂直偏移量，正值阴影在下侧
- blur-radius: 阴影模糊度，正值。值越大越模糊。
- separate-radius: 阴影扩展半径，可选参数。取正值，整个阴影扩展半径扩大，取负值，整个阴影扩展半径缩小。
- color: 阴影颜色，可选参数。

box-shadow 可以实现多层阴影，每层阴影都用逗号隔开。
