# HTML

## 块元素、行内元素

**行内元素**

-   a - 链接
-   abbr - 缩写
-   acronym - 首字
-   b - 粗体(不推荐)
-   bdo - 改变文字的显示顺序
-   big - 大字体
-   br - 换行
-   cite - 引用
-   code - 计算机代码(在引用源码的时候需要)
-   dfn - 定义字段
-   em - 强调
-   font - 字体设定(不推荐)
-   i - 斜体
-   img - 图片
-   input - 输入框
-   kbd - 定义键盘文本
-   label - 表格标签
-   q - 短引用
-   s - 中划线(不推荐)
-   samp - 定义范例计算机代码
-   select - 项目选择
-   small - 小字体文本
-   span - 常用内联容器，定义文本内区块
-   strike - 中划线
-   strong - 粗体强调
-   sub - 下标
-   sup - 上标
-   textarea - 多行文本输入框
-   tt - 电传文本
-   u - 下划线
-   var - 定义变量

**块元素**

-   address - 地址
-   blockquote - 块引用
-   center - 举中对齐块
-   dir - 目录列表
-   div - 常用块级容易，也是 css layout 的主要标签
-   dl - 定义列表
-   fieldset - form 控制组
-   form - 交互表单
-   h1 - 大标题
-   h2 - 副标题
-   h3 - 3 级标题
-   h4 - 4 级标题
-   h5 - 5 级标题
-   h6 - 6 级标题
-   hr - 水平分隔线
-   isindex - input prompt
-   menu - 菜单列表
-   noframes - frames 可选内容，（对于不支持 frame 的浏览器显示此区块内容
-   noscript - 可选脚本内容（对于不支持 script 的浏览器显示此内容）
-   ol - 排序表单
-   p - 段落
-   pre - 格式化文本
-   table - 表格
-   ul - 非排序列表

# CSS

## 使元素消失的方法有哪些？

### CSS 层面

-   opacity：0，该元素隐藏起来了，但不会改变页面布局，并且，如果该元素已经绑定一些事件，如 click 事件，那么点击该区域，也能触发点击事件的
-   visibility：hidden，该元素隐藏起来了，但不会改变页面布局，但是不会触发该元素已经绑定的事件
-   display：none，把元素隐藏起来，并且会改变页面布局，可以理解成在页面中把该元素删除掉

### JavaScript 层面

-   元素置空
-   删除节点

### CSS 盒模型

-   块级元素
-   行内元素

### 浮动

#### 清除浮动的方法

-   给要清除浮动的元素添加样式 clear，
-   父元素结束标签钱插入清除浮动的块级元素，给该元素添加样式 clear
-   添加伪元素，在父级元素的最后，添加一个伪元素，通过清除伪元素的浮动，注意该伪元素的 display 为 block，
-   父元素添加样式 overflow 清除浮动，overflow 设置除 visible 以外的任何位置

### 定位

-   元素居中的方法

# 网络协议

## HTTP

> 超文本传输协议

## HTTPS

## FTP

> 文件传输协议

## TCP/IP

> 传输控制协议

## UDP

> 用户数据报协议

# JavaScript

## 基本数据类型

**值类型(基本类型)**：

字符串（String）、数字(Number)、布尔(Boolean)、对空（Null）、未定义（Undefined）、唯一类型 Symbol。

##### **引用数据类型**：

对象(Object)、数组(Array)、函数(Function)。

## 深、浅拷贝

### 浅拷贝

> 如果数组元素是基本类型，就会拷贝一份，互不影响，而如果是对象或者数组，就会只拷贝对象和数组的引用，无论对新旧数组的哪一个进行了修改，两者都会发生变化。

#### 浅拷贝的方法

##### 数组

```javascript
var newArr = arr;
// "="
var newArr = arr.slice();
// slice()
var newArr = arr.concat();
// contact()
```

##### 对象

直接赋值

### 深拷贝

> 完全的拷贝一个对象，即使嵌套了对象，两者也相互分离，修改一个对象的属性，也不会影响另一个。

#### 深拷贝的方法

##### **JSON 序列化、反序列化**

```javascript
let newArr = JSON.parse(JSON.stringify(arr)); //解决
```

##### **自定义方法**

```javascript
var deepCopy = function (obj) {
    // 只拷贝对象
    if (typeof obj !== "object") return;
    // 根据obj的类型判断是新建一个数组还是一个对象
    var newObj = obj instanceof Array ? [] : {};
    for (var key in obj) {
        // 遍历obj,并且判断是obj的属性才拷贝
        if (obj.hasOwnProperty(key)) {
            // 判断属性值的类型，如果是对象递归调用深拷贝
            newObj[key] =
                typeof obj[key] === "object" ? deepCopy(obj[key]) : obj[key];
        }
    }
    return newObj;
};
```

## 内置基本构造函数

### Date

相关方法见[JavaScript Date Object.md](JavaScript Date Object.md)

### Array

相关方法见[JavaScript Array.md](./JavaScript Array.md)

### Object

相关方法见[JavaScript Object.md](./JavaScript Object.md)Object 对象

### Math

相关方法见[JavaScript Math Object.md](./JavaScript Math Object.md)Math 对象

## 垃圾回收机制

垃圾回收的具体应用

# 数据结构与算法

## 基本概念

## 常见算法

# Vue.js 全家桶

## Vue-Router

## VueX

## VueSSR

## Vue.config.js

见相关[Options VueConfig.md](./Options VueConfig.md)

## 原理

### 双向绑定的原理

>

### 路由跳转的原理

>

### 响应式原理

# React.js

## Lifecycle

16 以前 新旧版本区分版本号

### 新版

### 旧版

## 路由

## 相关 Api

## React Native

# Webpack

## 编译原理

## 配置项

见相关[Options Webpack.md](./Options Webpack.md)

# Nginx 服务器软件

#### 配置多端口访问

#### 配置 https 证书

# Linux 服务器操作系统

### 常用命令

见相关[Server Linux.md](./Server Linux.md)

# 项目相关

### 性能优化建议

### 服务器部署

### 浏览器兼容
