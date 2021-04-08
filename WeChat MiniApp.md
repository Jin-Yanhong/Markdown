## WXSS 样式

-   隐藏微信滚动条

```css
::-webkit-scrollbar {
    display: none;
    width: 0;
    height: 0;
    color: transparent;
}
```

## WXML 内容

-   隐藏微信滚动条

```html

```

## js 内容

-   data 动态赋值

```javascript
_this.setData({
    ['orderInfo[' + index + '].mwShoppingCartList']: hasEfficacy,
});
```
