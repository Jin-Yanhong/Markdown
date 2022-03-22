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

## Call()

> **`call()`** 方法使用一个指定的 `this` 值和单独给出的一个或多个参数来调用一个函数。

```javascript
function.call(thisArg, arg1, arg2, ...) // 参数列表
```

```javascript
function Product(name, price) {
    this.name = name;
    this.price = price;
}

function Food(name, price) {
    Product.call(this, name, price);
    this.category = "food";
}

console.log(new Food("cheese", 5).name);
// expected output: "cheese"
```

## Apply()

> **`apply()`** 方法调用一个具有给定`this`值的函数，以及以一个数组（或[类数组对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Indexed_collections#working_with_array-like_objects)）的形式提供的参数。

```javascript
func.apply(thisArg, [argsArray]);
```

```javascript
const numbers = [5, 6, 2, 3, 7];

const max = Math.max.apply(null, numbers);

console.log(max);
// expected output: 7

const min = Math.min.apply(null, numbers);

console.log(min);
// expected output: 2
```

## Bind()

> **`bind()`** 方法创建一个新的函数，在 `bind()` 被调用时，这个新函数的 `this` 被指定为 `bind()` 的第一个参数，而其余参数将作为新函数的参数，供调用时使用。

```javascript
function.bind(thisArg[, arg1[, arg2[, ...]]])
```

```javascript
const module = {
    x: 42,
    getX: function () {
        return this.x;
    },
};

const unboundGetX = module.getX;
console.log(unboundGetX()); // The function gets invoked at the global scope
// expected output: undefined

const boundGetX = unboundGetX.bind(module);
console.log(boundGetX());
// expected output: 42
```
