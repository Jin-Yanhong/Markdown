## CSS

### 高级选择器

#### 属性选择器

| 选择器                  | 描述                                                        |
| :---------------------- | :---------------------------------------------------------- |
| [_attribute_]           | 用于选取带有指定属性的元素。                                |
| [_attribute_=_value_]   | 用于选取带有指定属性和值的元素。                            |
| [_attribute_~=_value_]  | 用于选取属性值中包含指定词汇的元素。                        |
| [_attribute_\|=_value_] | 用于选取带有以指定值开头的属性值的元素,该值必须是整个单词。 |
| [_attribute_^=_value_]  | 匹配属性值以指定值开头的每个元素。                          |
| [_attribute_$=_value_]  | 匹配属性值以指定值结尾的每个元素。                          |
| [_attribute_*=_value_]  | 匹配属性值中包含指定值的每个元素。                          |

#### 子代选择器

```css
div > p {
    /* 直接子代 */
}
```

#### 奇偶选择器

```css
.child:nth-child(odd) {
    /* 奇数 */
}
.child:nth-child(even) {
    /* 偶数 */
}
```

#### 兄弟选择器

```css
div ~ p {
    /* 普通兄弟选择器 */
}
div + p {
    /* 相邻兄弟选择器 */
}
```

#### CSS 选择器穿透

vue 框架下深度选择器

```css
/deep/ div {
    /* 1 */
}
div >>> p {
    /* 2 */
}
div ::v-deep p {
    /* 3 */
}
```

### flex 布局

> 当元素表现为 flex 框时,它们沿着两个轴来布局：

![img](https://gitee.com/Coder-jin/PicStore/raw/master/flex-term.png)

-   **主轴（main axis）**是沿着 flex 元素放置的方向延伸的轴（比如页面上的横向的行、纵向的列）。该轴的开始和结束被称为 **main start** 和 **main end**。
-   **交叉轴（cross axis）**是垂直于 flex 元素放置方向的轴。该轴的开始和结束被称为 **cross start** 和 **cross end**。
-   设置了 `display: flex` 的父元素（在本例中是 [`<section>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/section)）被称之为 **flex 容器（flex container）。**
-   在 flex 容器中表现为柔性的盒子的元素被称之为 **flex 项**（**flex item**）

#### 相关 CSS 属性

##### 容器元素的属性

```css
.farther {
    /* 用来指定主轴的方向 */
    flex-direction: row | row-reverse | column | column-reverse;

    /* 是否折行 */
    flex-wrap: nowrap | wrap | wrap-reverse;
    /* wrap-reverse 垂直于主轴的方向排列发生变化 */
    /* ==> 简写为 */
    flex-flow: <flex-direction> || <flex-wrap>; /* 默认值为 row nowrap */

    /* justify-content 指定主轴上的对齐方式 */
    justify-content: flex-start | flex-end | center | space-between |
        space-around|space-evenly;
    /* space-between: 基于容器平均分布;语素与容器间隔为0 */
    /* space-around: 基于item平均分布;元素间间隔相等 */
    /* space-evenly: 基于内容平均分布;语素与容器、元素间间隔相等 */

    /* align-items属性定义item在交叉轴上如何对齐。 */
    align-items: flex-start | flex-end | center | baseline | stretch;
    /* baseline: item的第一行文字的基线对齐。 */
    /* stretch（默认值）：如果item未设置高度或设为auto,将占满整个容器的高度。 */

    /* align-content属性定义了多根轴线（多行）的对齐方式。如果item只有一根轴线,该属性不起作用。 */
    align-content: flex-start | flex-end | center | space-between | space-around
        | stretch;
}
```

##### 内部元素的属性

```css
.child_A {
    /* 指定每个item的占主轴的比例 */

    /* order属性定义item的排列顺序。数值越小,排列越靠前,默认为0。 */
    order: <integer>;

    /* flex-grow属性定义item的放大比例,默认为0,即如果存在剩余空间,也不放大。
    如果所有item的flex-grow属性都为1,则它们将等分剩余空间（如果有的话）。如果一个item的flex-grow属性为2,其他item都为1,则前者占据的剩余空间将比其他项多一倍。 */
    flex-grow: <number>; /* default 0 */

    /* 同 flex-grow,缩小 */
    flex-shrink: <number>; /* default 1 */

    /* flex-basis 指定了 flex 元素在主轴方向上的初始大小。如果不使用  box-sizing 改变盒模型的话,那么这个属性就决定了 flex 元素的内容盒（content-box）的尺寸。 */
    flex-basis: <length> | auto; /* default auto */

    /* 上述属性的简写 */
    flex: none | [ < "flex-grow" > < "flex-shrink" >? || < "flex-basis" > ];

    /* align-self 会对齐当前 grid 或 flex 行中的元素,并覆盖已有的 align-items 的值 */
    align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```

### gird 布局

##### 容器元素的属性

```css
.farther {
    /* 指定grid布局 */
    display: grid|inline-grid;
    /* 指定行数、列数,后边的值也可以是百分数*/
    grid-template-columns: 100px 100px 100px;
    grid-template-rows: 33.33% 33.33% 33.33%;
    /* 也可以使用 repeat() 函数 */
    /* repeat()接受两个参数,第一个参数是重复的次数（上例是3）,第二个参数是所要重复的值。 */
    grid-template-columns: repeat(3, 33.33%);
    grid-template-rows: repeat(3, 33.33%);
    /* 为了方便表示比例关系,网格布局提供了fr关键字（fraction 的缩写,意为"片段"）。如果两列的宽度分别为1fr和2fr,就表示后者是前者的两倍。 */
    grid-template-columns: 1fr 1fr; /* 表示两个相同的列 */
    /* 也可以组合使用 */
    grid-template-columns: 150px 1fr 2fr;
    /* minmax()函数产生一个长度范围,表示长度就在这个范围之中。它接受两个参数,分别为最小值和最大值。 */
    grid-template-columns: 1fr 1fr minmax(100px, 1fr);
    /* auto关键字表示由浏览器自己决定长度。 */
    grid-template-columns: 100px auto 100px;
    /* 可以使用方括号,指定每一根网格线的名字,方便以后的引用 */
    grid-template-columns: [c1] 100px [c2] 100px [c3] auto [c4];
    grid-template-rows: [r1] 100px [r2] 100px [r3] auto [r4];
    /* 上面代码指定网格布局为3行 x 3列,因此有4根垂直网格线和4根水平网格线。方括号里面依次是这八根线的名字。 */
    /* 网格布局允许同一根线有多个名字,比如[fifth-line row-5] */

    /* 分别指定行间距、列间距 */
    row-gap: 20px;
    column-gap: 20px;
    /* 简写为 */
    gap: <row-gap> <column-gap>;

    grid-template-areas: "详细说明";

    /* 改变元素的自动排列方式 */
    grid-auto-flow: | row| column| dense| row dense| column dense;
    /* dense:优先填补空白; */
    /* row dense:先行后列; */
    /* column dense:先列后行; */

    /* 水平方向对齐方式 */
    justify-items: start | end | center | stretch;
    /* 垂直方向对齐方式 */
    align-items: start | end | center | stretch;
    /* 简写 */
    place-items: <align-items> <justify-items>;
    /* start：对齐单元格的起始边缘。 */
    /* end：对齐单元格的结束边缘。 */
    /* center：单元格内部居中。 */
    /* stretch：拉伸,占满单元格的整个宽度（默认值）。 */

    /* justify-content属性是整个内容区域在容器里面的水平位置（左中右） */
    justify-content: start | end | center | stretch | space-around |
        space-between | space-evenly;
    /* align-content属性是整个内容区域的垂直位置（上中下） */
    align-content: start | end | center | stretch | space-around | space-between
        | space-evenly;
    /* 简写为 */
    place-content: <align-content> <justify-content>;
}
```

> 设为网格布局以后,容器子元素（项目）的 float、display: inline-block、display: table-cell、vertical-align 和 column-\*等设置都将失效

> -   **repeat()重复某种模式也是可以的。**
>
> ```css
> .container {
>     display: grid;
>     grid-template-columns: repeat(2, 100px 20px 80px);
> }
> ```
>
> 得到如下的情形
>
> <div><img src="https://gitee.com/Coder-jin/PicStore/raw/master/bg2019032507.png"></div>
>
> ---
>
> -   **有时,单元格的大小是固定的,但是容器的大小不确定。如果希望每一行（或每一列）容纳尽可能多的单元格,这时可以使用 `auto-fill` 关键字表示自动填充。**
>
> ```css
> .container {
>     display: grid;
>     grid-template-columns: repeat(auto-fill, 100px);
> }
> ```
>
> 得到如下的情形
>
> <div><img src="https://gitee.com/Coder-jin/PicStore/raw/master/bg2019032508.png"></div>
>
> ---
>
> -   **`grid-template-areas` 详细描述**
>
> ```css
> .container {
>     display: grid;
>     grid-template-columns: 100px 100px 100px;
>     grid-template-rows: 100px 100px 100px;
>     grid-template-areas:
>         "a b c"
>         "d e f"
>         "g h i";
> }
> ```
>
> 上面代码先划分出 9 个单元格,然后将其定名为`a`到`i`的九个区域,分别对应这九个单元格。
>
> 多个单元格合并成一个区域的写法如下。
>
> ```css
> .container {
>     grid-template-areas:
>         "a a a"
>         "b b b"
>         "c c c";
> }
> ```
>
> 上面代码将 9 个单元格分成`a`、`b`、`c`三个区域
> 如果某些区域不需要利用,则使用"点"（`.`）表示。
>
> ```css
> .container {
>     grid-template-areas:
>         "a . c"
>         "d . f"
>         "g . i";
> }
> ```
>
> 上面代码中,中间一列为点,表示没有用到该单元格,或者该单元格不属于任何区域。
>
> 注意,区域的命名会影响到网格线。每个区域的起始网格线,会自动命名为`区域名-start`,终止网格线自动命名为`区域名-end`。
>
> 比如,区域名为`header`,则起始位置的水平网格线和垂直网格线叫做`header-start`,终止位置的水平网格线和垂直网格线叫做`header-end`。

##### 内部元素的属性

```css
.child_A {
    /* 制定内部元素的起始位置 */
    grid-column-start: ""; /* 左边框所在的垂直网格线 */
    grid-column-end: ""; /* 右边框所在的垂直网格线 */
    grid-row-start: ""; /* 上边框所在的水平网格线 */
    grid-row-end: ""; /* 下边框所在的水平网格线 */

    /* 除了指定为第几个网格线,还可以指定为网格线的名字。 */
    grid-column-start: header-start;
    grid-column-end: header-end;
    /* 还可以使用span关键字,表示"跨越",即左右边框（上下边框）之间跨越多少个网格。 */
    grid-column-start: span 2;
    /* ==> */
    grid-column-end: span 2;

    /* 行列的属性合并 */
    grid-column: <start-line> | <end-line>;
    grid-row: <start-line> | <end-line>;

    /* 指定元素所在的位置区域 */
    grid-area: a;
    /* ==> */
    grid-area: <row-start> | <column-start> | <row-end> | <column-end>;

    /* justify-self 设置单元格内容的水平位置（左中右）,跟justify-items属性的用法完全一致,但只作用于单个项目。 */
    justify-self: "";
    /* align-self属性设置单元格内容的垂直位置（上中下）,跟align-items属性的用法完全一致,也是只作用于单个项目。 */
    align-self: "";
    /* ==> place-self */
    place-self: <align-self> <justify-self>;
}
```

## 媒体查询

### 适应不同尺寸的屏幕

```css
.example {
    /*  */
}
/* Extra small devices (phones, 600px and down) */
@media only screen and (max-width: 600px) {
    .example {
        /*  */
    }
}

/* Small devices (portrait tablets and large phones, 600px and up) */
@media only screen and (min-width: 600px) {
    .example {
        /*  */
    }
}

/* Medium devices (landscape tablets, 768px and up) */
@media only screen and (min-width: 768px) {
    .example {
        /*  */
    }
}

/* Large devices (laptops/desktops, 992px and up) */
@media only screen and (min-width: 992px) {
    .example {
        /*  */
    }
}

/* Extra large devices (large laptops and desktops, 1200px and up) */
@media only screen and (min-width: 1200px) {
    .example {
        /*  */
    }
}
```

### 横屏\竖屏

```css
@media only screen and (orientation: landscape) {
    body {
        background-color: lightblue;
    }
}
```

## 动画

### 定义 css 关键帧

```css
@keyframes animated_div {
    0% {
        transform: rotate(0deg);
        left: 0px;
    }
    25% {
        transform: rotate(20deg);
        left: 0px;
    }
    50% {
        transform: rotate(0deg);
        left: 500px;
    }
    55% {
        transform: rotate(0deg);
        left: 500px;
    }
    70% {
        transform: rotate(0deg);
        left: 500px;
        background: #1ec7e6;
    }
    100% {
        transform: rotate(-360deg);
        left: 0px;
    }
}
/* 动画的调用 */
.div {
    animation: animated_div 3s;
}
```

属性列表如下

| 属性                      | 描述                                                                                   |
| :------------------------ | :------------------------------------------------------------------------------------- |
| @keyframes                | 规定动画。                                                                             |
| animation                 | 所有动画属性的简写属性。                                                               |
| animation-name            | 规定 @keyframes 动画的名称。                                                           |
| animation-duration        | 规定动画完成一个周期所花费的秒或毫秒。默认是 0。                                       |
| animation-timing-function | 规定动画的速度曲线。默认是 "ease"。                                                    |
| animation-fill-mode       | 规定当动画不播放时（当动画完成时,或当动画有一个延迟未开始播放时）,要应用到元素的样式。 |
| animation-delay           | 规定动画何时开始。默认是 0。                                                           |
| animation-iteration-count | 规定动画被播放的次数。默认是 1。                                                       |
| animation-direction       | 规定动画是否在下一周期逆向地播放。默认是 "normal"。                                    |
| animation-play-state      | 规定动画是否正在运行或暂停。默认是 "running"。                                         |

### 路径动画

```css
div {
    /* 只改变运动路径,其他保持一致 */
    offset-path: path(
        "M 0 0 L 100 0 L 200 0 L 300 100 L 400 0 L 500 100 L 600 0 L 700 100 L 800 0"
    );
    animation: move 2000ms infinite alternate linear;
}
@keyframes move {
    0% {
        offset-distance: 0%;
    }
    100% {
        offset-distance: 100%;
    }
}
```

## SVG 矢量动画

-   [ ] [超级强大的 SVG SMIL animation 动画详解](https://www.zhangxinxu.com/wordpress/2014/08/so-powerful-svg-smil-animation/)

-   [ ] [纯 CSS 实现帅气的 SVG 路径描边动画效果](https://www.zhangxinxu.com/wordpress/2014/04/animateion-line-drawing-svg-path-%e5%8a%a8%e7%94%bb-%e8%b7%af%e5%be%84/)

## 3D 变形

属性如下：

| 属性                                                                                 | 描述                                 |
| :----------------------------------------------------------------------------------- | :----------------------------------- |
| [transform](https://www.w3school.com.cn/cssref/pr_transform.asp)                     | 向元素应用 2D 或 3D 转换。           |
| [transform-origin](https://www.w3school.com.cn/cssref/pr_transform-origin.asp)       | 允许你改变被转换元素的位置。         |
| [transform-style](https://www.w3school.com.cn/cssref/pr_transform-style.asp)         | 规定被嵌套元素如何在 3D 空间中显示。 |
| [perspective](https://www.w3school.com.cn/cssref/pr_perspective.asp)                 | 规定 3D 元素的透视效果。             |
| [perspective-origin](https://www.w3school.com.cn/cssref/pr_perspective-origin.asp)   | 规定 3D 元素的底部位置。             |
| [backface-visibility](https://www.w3school.com.cn/cssref/pr_backface-visibility.asp) | 定义元素在不面对屏幕时是否可见。     |

transform：

```css
.div {
    transform: ;
    /* 2d、3d、旋转、变形、缩放 */
}
```

| 值                              | 描述                                   |
| :------------------------------ | :------------------------------------- |
| none                            | 定义不进行转换。                       |
| matrix(_n_,_n_,_n_,_n_,_n_,_n_) | 定义 2D 转换,使用六个值的矩阵。        |
| matrix3d()                      | 定义 3D 转换,使用 16 个值的 4x4 矩阵。 |
| translate(_x_,_y_)              | 定义 2D 转换。                         |
| translate3d(_x_,_y_,_z_)        | 定义 3D 转换。                         |
| translateX(_x_)                 | 定义转换,只是用 X 轴的值。             |
| translateY(_y_)                 | 定义转换,只是用 Y 轴的值。             |
| translateZ(_z_)                 | 定义 3D 转换,只是用 Z 轴的值。         |
| scale(_x_,_y_)                  | 定义 2D 缩放转换。                     |
| scale3d(_x_,_y_,_z_)            | 定义 3D 缩放转换。                     |
| scaleX(_x_)                     | 通过设置 X 轴的值来定义缩放转换。      |
| scaleY(_y_)                     | 通过设置 Y 轴的值来定义缩放转换。      |
| scaleZ(_z_)                     | 通过设置 Z 轴的值来定义 3D 缩放转换。  |
| rotate(_angle_)                 | 定义 2D 旋转,在参数中规定角度。        |
| rotate3d(_x_,_y_,_z_,_angle_)   | 定义 3D 旋转。                         |
| rotateX(_angle_)                | 定义沿着 X 轴的 3D 旋转。              |
| rotateY(_angle_)                | 定义沿着 Y 轴的 3D 旋转。              |
| rotateZ(_angle_)                | 定义沿着 Z 轴的 3D 旋转。              |
| skew(_x-angle_,_y-angle_)       | 定义沿着 X 和 Y 轴的 2D 倾斜转换。     |
| skewX(_angle_)                  | 定义沿着 X 轴的 2D 倾斜转换。          |
| skewY(_angle_)                  | 定义沿着 Y 轴的 2D 倾斜转换。          |
| perspective(_n_)                | 为 3D 转换元素定义透视视图。           |

## css 代码片段

### 动画变形

#### 透视变形

```css
.obj {
    transform: perspective(1000px) rotateY(45deg);
}
```

### 本文美化

#### 文本溢出显示省略号

```css
// 单行溢出隐藏
p {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
// 多行显示省略号
p {
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 3;
    overflow: hidden;
}
```

#### 调整 Chromium 内核浏览器滚动条

```css
/* 滚动条 */
.container::-webkit-scrollbar {
    -webkit-box-shadow: #48a7ff !important;
    width: 10px;
    height: 10px;
}

/* 滚动槽 */
.container::-webkit-scrollbar-track {
    -webkit-box-shadow: #48a7ff !important;
    border-radius: 10px;
    background: #114a7f;
}

/* 滚动条滑块 */
.container::-webkit-scrollbar-thumb {
    border-radius: 10px;
    background: #48a7ff;
    -webkit-box-shadow: #48a7ff;
}
```

#### 标签内文本均匀分布

```css
p {
    text-align-last: justify;
}
```

#### 利用伪元素做四个角的边框

```less
.borderBg {
    position: absolute;
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    border: 1px solid #56fdfb;
    width: 100%;
    top: 38px;
    left: 0;
    height: calc(100% - 35px);
    box-shadow: 0 0 40px 0 #188ee7 inset;
}
.borderBg::before {
    display: block;
    position: absolute;
    content: "";
    left: -1px;
    top: 23px;
    width: calc(100% + 2px);
    height: calc(100% - 46px);
    border-left: 1px solid #325886;
    border-right: 1px solid #325886;
    z-index: 10;
}
.borderBg::after {
    display: block;
    position: absolute;
    content: "";
    top: -1px;
    left: 23px;
    height: calc(100% + 2px);
    width: calc(100% - 46px);
    border-top: 1px solid #325886;
    border-bottom: 1px solid #325886;
    z-index: 10;
}
```

## CSS in JS

### var()

> -   IE 无效,其余主流浏览器有效
> -   [介绍与使用详情(MDN)](https://developer.mozilla.org/zh-CN/docs/Web/CSS/var)

### var()使用

> -   只能在{}内声明,作用范围由{}的选择器决定
> -   CSS 中原生的变量定义语法 **`参考文档，后续更新`**

### 运行时改变 scss 变量值

> -   简单来说就是将 scss 的变量交由 css 变量控制
> -   参考[css4-variables-and-sass](https://codepen.io/jakealbaugh/post/css4-variables-and-sass)

### 示例

```scss
$colors: (
    primary: #ffbb00,
    secondary: #0969a2,
);

Selector1 {
    @each $name, $color in $colors {
        --color-#{$name}: $color;
    }
}

// Selector1的生成效果
:root {
    --color-primary: #ffbb00;
    --color-secondary: #0969a2;
}

// 使用方式一 直接使用css变量
Selector {
    color: var(--color-primary);
}

// 使用方式二 利用scss的函数, 以符合scss语法 推荐
@function color($color-name) {
    @return var(--color-#{$color-name});
}

body {
    color: color(primary); //使用
}

// body生成效果
body {
    color: var(--color-primary); //这样就可以被js设置了
}
```

```scss
/* 声明 */
body {
    /* body内有效 */
    --name: value;
}

/* 使用 */
.test {
    /* 当--name不存在时,使用defaultValue */
    attr: var(--name,defaultValue)
    /* 错误的使用方法 */
    var(--name): #369;
}

```

### js 设置 css 变量

即设置运行 scss 变量

```javascript
// domObject => dom 节点
domObject.style.setProperty(name, value); //name为css变量名 e.g: --color-primary
```

> 由于 scss 是预编译的,无法在运行时改变变量值,而我又需要去改变,所以去 google 了,得到一个满意的解决方案 [原理(English)](https://codepen.io/jakealbaugh/post/css4-variables-and-sass)
>
> 像这种的,变量–test 根本找不到,理由是并没有这个 root,vue 组件 scoped 的特性,只在本组件有效,但组件又没有完整的 document,即组件内部没有 root
