# JavaScript 模块化规范

## AMD 规范

Asynchronous Module Definition （异步模块定义规范）

### 导出

```javascript
define([], function () {
    return {
        hello: function () {
            console.log('hello');
        },
        goodbye: function () {
            console.log('goodbye');
        },
    };
});
```

> 通过 **`define`** 关键字 定义相关模块

### 导入

```javascript
define(['myModule', 'myOtherModule'], function (myModule, myOtherModule) {
    console.log(myModule.hello());
});
```

**`说明`**：这里我们使用 define 方法，第一个参数是依赖的模块，这些模块都会在后台无阻塞地加载，第二个参数则作为加载完毕的回调函数。回调函数将会使用载入的模块作为参数。在这个例子里就是 myMoudle 和 myOtherModule

### 注意：

> AMD 浏览器优先、异步载入

> AMD 的另一个优点是你可以在模块里使用对象、函数、构造函数、字符串、JSON 或者别的数据类型，而 CommonJS 只支持对象。

> AMD 不支持 Node 里的一些诸如 IO,文件系统等其他服务器端的功能。另外语法上写起来也比 CommonJS 麻烦一些

## Common JS 规范

CommonJS 扩展了 JavaScript 声明模块的 API

Node.js 广泛使用

### 导出

```javascript
function myModule() {
    this.hello = function () {
        return 'hello!';
    };
    this.goodbye = function () {
        return 'goodbye!';
    };
}
module.exports = myModule;
```

### 导入

```javascript
var myModule = require('myModule');
var myModuleInstance = new myModule();
myModuleInstance.hello(); // 'hello!'
myModuleInstance.goodbye(); // 'goodbye!'
```

### 注意

> CommonJS 以**`服务器优先`**的方式来同步载入模块，假使我们引入三个模块的话，他们会一个个地被载入。
>
> 同步 加载模块 阻塞 主进程

## ES6 规范

### 导出

-   混合导出

```javascript
export { module1 as default, module2, module3 };
```

-   批量导出

```javascript
export { module1, module2, module3 };
```

-   设置别名

```javascript
export { module1 as module2, module3, module4 };
```

### 导入

-   批量导入

```javascript
import{ module1 as default, module2, module3 } from "./..."
```

-   设置别名

```javascript
import module1 as module2  from "./..."
```

-   混合导入

```javascript
import { module1 as module2, module3, module4 } from './...';
```

### 技巧

> **`ES6 规范是实时只读的`**

# 以下模块化不常用

## UMD 规范

Universal Module Definition（通用模块定义规范）

### 导出

### 导入

### 注意

> UMD 创造了一种同时使用两种规范的方法，并且也支持全局变量定义。所以 UMD 的模块可以同时在客户端和服务端使用。
