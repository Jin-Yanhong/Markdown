## CSS

### 高级选择器

```css
div {
}
```

#### 属性选择器

| 选择器                  | 描述                                                         |
| :---------------------- | :----------------------------------------------------------- |
| [_attribute_]           | 用于选取带有指定属性的元素。                                 |
| [_attribute_=_value_]   | 用于选取带有指定属性和值的元素。                             |
| [_attribute_~=_value_]  | 用于选取属性值中包含指定词汇的元素。                         |
| [_attribute_\|=_value_] | 用于选取带有以指定值开头的属性值的元素，该值必须是整个单词。 |
| [_attribute_^=_value_]  | 匹配属性值以指定值开头的每个元素。                           |
| [_attribute_$=_value_]  | 匹配属性值以指定值结尾的每个元素。                           |
| [_attribute_*=_value_]  | 匹配属性值中包含指定值的每个元素。                           |

#### 子代选择器

```css
div > p {
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

```css
/deep /div {
}
```

### flex 布局

> 当元素表现为 flex 框时，它们沿着两个轴来布局：

![flex_terms.png](https://gitee.com/Coder-jin/PicStore/raw/master/flex_terms.png)

-   **主轴（main axis）**是沿着 flex 元素放置的方向延伸的轴（比如页面上的横向的行、纵向的列）。该轴的开始和结束被称为 **main start** 和 **main end**。
-   **交叉轴（cross axis）**是垂直于 flex 元素放置方向的轴。该轴的开始和结束被称为 **cross start** 和 **cross end**。
-   设置了 `display: flex` 的父元素（在本例中是 [`<section>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/section)）被称之为 **flex 容器（flex container）。**
-   在 flex 容器中表现为柔性的盒子的元素被称之为 **flex 项**（**flex item**）

#### 相关 CSS 属性

#### Code_Snip

```css
.farther {
    /* 用来指定主轴的方向 */
    /* 注意：可以使用 row-reverse 和 column-reverse 值反向排列 flex 项目 */
    flex-direction: column;
    /* 是否折行 */
    flex-wrap: wrap;
    /* ==> 简写为 */
    flex-flow: column, wrap;
}
.child_A {
    /* 指定每个item的占主轴的比例 */
    flex: 1 200px;
}
.child_B {
    /* 指定每个item的占主轴的比例 */
    flex: 2 200px;
}
```

> 每个 flex 项将首先给出 200px 的可用空间，然后，剩余的可用空间将根据分配的比例共享

#### 全写与缩写

```css
/* 建议简写，除非是覆盖原有值 */
.child {
    flex: 1 0 10px;
}
```

> -   第一个就是上面所讨论过的无单位比例。可以单独指定全写 `flex-grow` 属性的值。
> -   第二个无单位比例 `flex-shrink` 一般用于溢出容器的 flex 项。这指定了从每个 flex 项中取出多少溢出量，以阻止它们溢出它们的容器。 这是一个相当高级的弹性盒子功能，我们不会在本文中进一步说明。
> -   第三个是上面讨论的最小值。可以单独指定全写 `flex-basis` 属性的值。

### gird 布局

>

### 盒模型

#### 浮动

>

##### 浮动的影响

>

##### 清除浮动

>

#### 定位

>

#### 绝对定位

>

#### 相对定位

>

#### 固定定位

>

#### Code_Snip

>

## 媒体查询

>

## 动画

>

## 3D 变形

>
