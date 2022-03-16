## Html 结构

```html
<div class="container">
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
    <div class="item">4</div>
    <div class="item">5</div>
    <div class="item">6</div>
    <div class="item">7</div>
    <div class="item">8</div>
    <div class="item">9</div>
</div>
```

## CSS 样式

```css
.container {
    display: grid;
    grid-template-rows: [r1] 100px [r2] 100px [r3] auto [r4];
    /* grid-template-rows: repeat(3, 33.33%); */
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    /* grid-template-columns: repeat(auto-fill, minmax(240px, 1fr)); */
    /* grid-template-columns: repeat(3, 33.33%); */
    /* grid-template-columns: 150px 1fr 2fr; */
    /* grid-template-columns: repeat(2, 100px 20px 80px); */
    /* grid-template-columns: 1fr 1fr minmax(100px, 1fr); */
    /* grid-template-columns: [c1] 100px [c2] 100px [c3] auto [c4]; */
    /* 其中 [] 用于给边界线命名，相当于别名*/

    /* grid-row-gap用于设置行间距，grid-column-gap用于设置列间距。 */
    /* row-gap: 20px;
    column-gap: 20px; */
    /* 相当于 */
    gap: 20px 20px;

    grid-template-areas:
        "a b c"
        "d e f"
        "g h i";
    /* 如果某些区域不需要利用，则使用"点"（.）表示。 */
    /* grid-template-areas:
                    'a . c'
                    'd . f'
                    'g . i'; */

    /* grid-auto-flow: column; 默认 row */

    grid-auto-flow: row dense; /* 表示"先行后列"，并且尽可能紧密填满，尽量不出现空格。 */
    grid-auto-flow: column dense; /* 表示"先列后行"，并且尽量填满空格。 */

    /* 单元格的内容对齐方式 */
    /* justify-items: start | end | center | stretch; */
    justify-items: start;
    /* 单元格的内容头部对齐 */
    /* align-items: start | end | center | stretch; */
    align-items: start;
    /* place-items属性是align-items属性和justify-items属性的合并简写形式。 */
}

.item {
    /* 定义行、列的起止边界 */
    grid-row-start: 1;
    grid-row-end: 3;
    grid-column-start: 1;
    grid-column-end: 3;

    /* 简写为 */
    /* grid-row: s-gridLine / e-gridLine; */
    /* grid-column: s-gridLine / e-gridLine; */
    /* span 偏移量 */
    /* grid-column: s-gridLine / span n ; */

    /* 元素在容器中所占用的区域，需要在容器中 设置 grid-template-areas 属性 */
    /* grid-area: 'a b c'; */
}
```
