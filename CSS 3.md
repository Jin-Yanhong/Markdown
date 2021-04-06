## HML5


```html

```

## CSS3


### 清除浮动

-   父级元素 after 伪元素设置如下 CSS：

```css
.dad::after {
    content: '\0020';
    display: block;
    height: 0;
    overflow: hidden;
    clear: both;
}
```

### flex 布局

- 内容上下左右居中
  
  父容器

```css
#dad {
  display: flex;
  justify-content: center;
  align-items: center
}
  
```

​	子容器

### vue 动态引入背景图片

```vue
:style="{ backgroundImage: 'url(' + item.imgsrc + ')', backgroundSize: '100% 100%',
backgroundRepeat: 'no-repeat', }"
```

### Grid 布局

### 清除滚动条

```
::-webkit-scrollbar {
  display:none;
  width:0;
  height:0;
  color:transparent;
}
```



### 定义字体

```css
span{
    /* 定义字体 */
    font:bold italic 45px/1.5rem 'Courier New' monospace 
}
```

