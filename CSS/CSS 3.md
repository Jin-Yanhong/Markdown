## 高级选择器

### 属性选择器

| 选择器              | 描述                                                         |
| :------------------ | :----------------------------------------------------------- |
| [attribute]         | 用于选取带有指定属性的元素。                                 |
| [attribute=value]   | 用于选取带有指定属性和值的元素。                             |
| [attribute~=value]  | 用于选取属性值中包含指定词汇的元素。                         |
| [attribute\|=value] | 用于选取带有以指定值开头的属性值的元素，该值必须是整个单词。 |
| [attribute^=value]  | 匹配属性值以指定值开头的每个元素。                           |
| [attribute$=value]  | 匹配属性值以指定值结尾的每个元素。                           |
| [attribute*=value]  | 匹配属性值中包含指定值的每个元素。                           |

### 子代选择器

```css
/* 直接子代 */
div > p {
}
```

### 奇偶选择器

```css
.child:nth-child(odd) {
	/* 奇数 */
}
.child:nth-child(even) {
	/* 偶数 */
}
```

### 兄弟选择器

```css
/* 普通兄弟选择器 */
div ~ p {
}
/* 相邻兄弟选择器 */
div + p {
}
```

## 媒体查询

#### 适应不同尺寸的屏幕

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

#### 横屏\竖屏

```css
@media only screen and (orientation: landscape) {
	body {
		background-color: lightblue;
	}
}
```

## css 代码片段

### 特殊滤镜

#### 界面黑白

```css
:-webkit-full-screen {
	-webkit-filter: grayscale(1);
	filter: grayscale(1);
}
:-ms-fullscreen {
	filter: grayscale(1);
}
:fullscreen {
	-webkit-filter: grayscale(1);
	filter: grayscale(1);
}
.disabled {
	-webkit-filter: grayscale(100%);
	-moz-filter: grayscale(100%);
	-ms-filter: grayscale(100%);
	-o-filter: grayscale(100%);
	filter: grayscale(100%);
	filter: gray;
	cursor: not-allowed !important;
}
html {
	/*兼容FF*/
	filter: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg'><filter id='grayscale'><feColorMatrix type='matrix' values='0.3333 0.3333 0.3333 0 0 0.3333 0.3333 0.3333 0 0 0.3333 0.3333 0.3333 0 0 0 0 0 1 0'/></filter></svg>#grayscale");
	/*兼容IE内核*/
	filter: progid:DXImageTransform.Microsoft.BasicImage(grayscale=1);
	/*兼容其它，谷歌之类的*/
	-webkit-filter: grayscale(1);
}
```

### 页面布局

#### 清除浮动

```css
.nav::after {
	content: '';
	clear: both;
	display: table;
}
```

#### 元素居中

##### 绝对定位居中

```css
div {
	position: absolute;
	left: 0;
	top: 0;
	right: 0;
	bottom: 0;
	margin: auto;
}
```

##### flex 布局居中

```css
.container {
	display: flex;
	justify-content: center;
	align-items: center;
}
```

##### table 布局居中

```html
<style>
	.center td {
		height: 500px;
		width: 500px;
		text-align: center;
		vertical-align: middle;
	}
</style>
<table border="1" class="center">
	<tr>
		<td>Text</td>
		<td>Text</td>
	</tr>
</table>
```

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
// 保持空白正常换行
p {
	word-wrap: pre-wrap;
}
```

#### 标签内文本均匀分布

```css
p {
	text-align-last: justify;
}
```

#### 文本不换行

```css
p {
	text-align-last: justify;
}
```

### 调整滚动条

```css
/* 滚动条 */
.container::-webkit-scrollbar {
	-webkit-box-shadow: [[48a7ff]] !important;
	width: 10px;
	height: 10px;
}

/* 滚动槽 */
.container::-webkit-scrollbar-track {
	-webkit-box-shadow: [[48a7ff]] !important;
	border-radius: 10px;
	background: [[114a7f]];
}

/* 滚动条滑块 */
.container::-webkit-scrollbar-thumb {
	border-radius: 10px;
	background: [[48a7ff]];
	-webkit-box-shadow: [[48a7ff]];
}
```

### 伪元素四角边框

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
	content: '';
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
	content: '';
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
