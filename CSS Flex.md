### flex 布局

> 当元素表现为 flex 框时,它们沿着两个轴来布局：

![img](https://gitee.com/Coder-jin/PicStore/raw/master/flex-term.png)

-   **主轴（main axis）**是沿着 flex 元素放置的方向延伸的轴（比如页面上的横向的行、纵向的列）。该轴的开始和结束被称为 **main start** 和 **main end**。
-   **交叉轴（cross axis）**是垂直于 flex 元素放置方向的轴。该轴的开始和结束被称为 **cross start** 和 **cross end**。
-   设置了 `display: flex` 的父元素，被称之为 **flex 容器（flex container）。**
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
