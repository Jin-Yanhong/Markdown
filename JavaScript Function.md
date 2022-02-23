## 函数的递归

## 函数的闭包

## 函数的返回值

## 函数的作用域

## 生成器函数

> **`function*`** 这种声明方式(`function`关键字后跟一个星号）会定义一个**_生成器函数\* (_**generator function**\*)**，它返回一个 [`Generator`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Generator) 对象。

```javascript
function* generator(i) {
    yield i;
    yield i + 10;
}

const gen = generator(10);

console.log(gen.next().value);
// expected output: 10

console.log(gen.next().value);
// expected output: 20
```
