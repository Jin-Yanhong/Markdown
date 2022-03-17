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

## js 内容

### Data Object

```javascript
_this.setData({
    ["orderInfo[" + index + "].mwShoppingCartList"]: hasEfficacy,
});
```

### 富文本

#### 改变富文本的文本样式

```javascript
.replace(/style\s*?=\s*?(['"])[\s\S]*?\1/gi, '')
.replace(/\<img/gi, '<img style="display:block;width:100%;margin:20px auto;"')
.replace(/\<p/gi, '<p class="p_richText"');
```

```css
.p_richText {
    /**/
}
```

### 微信 Api

#### 微信扫一扫

```javascript
// 普通页面  onLoad:
Page({
    onLoad: function (options) {
        if (options.scene) {
            const shopCode = decodeURIComponent(options.scene);
        }
    },
});

//  App.js (待验证)
Page({
    onLoad: function (options) {
        if (options?.query?.scene) {
            const shopCode = decodeURIComponent(options.query.scene);
        }
    },
});
```
