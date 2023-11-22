## 解构赋值

### 数组的解构赋值

#### 默认值

> 数组的元素是按次序排列的，变量的取值由它的位置决定

解构赋值允许指定默认值。

> ES6 内部使用严格相等运算符（`===`），判断一个位置是否有值。所以，只有当一个数组成员严格等于`undefined`，默认值才会生效。

```javascript
let [x = 1] = [undefined];
x; // 1

let [x = 1] = [null];
x; // null
```

#### 惰性赋值

如果默认值是一个表达式，那么这个表达式是惰性求值的，即只有在用到的时候，才会求值。

```javascript
function f() {
	console.log('aaa');
}

let [x = f()] = [1];
```

#### Tips

对象数组快速统一修改某一属性的值

```javascript
let todoList = [
	{
		index: 1,
		name: 'code',
		status: 'doing',
	},
];
let newTodoList = todoList.map((el, index) => {
	return { ...el, status: 'done' };
});
console.log(newTodoList);
// [{ index: 1, name: 'code', status: 'done' }]
```

### 对象的解构赋值

> 对象的解构与数组有一个重要的不同。而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。如果解构失败，得到的值为 **`undefined`**

如果变量名与属性名不一致，必须写成下面这样。

```javascript
let { foo: baz } = { foo: 'aaa', bar: 'bbb' };
baz; // "aaa"

let obj = { first: 'hello', last: 'world' };
let { first: f, last: l } = obj;
f; // 'hello'
l; // 'world'
```

> 与数组一样，解构也可以用于嵌套结构的对象。
>
> ```javascript
> let obj = {
> 	p: ['Hello', { y: 'World' }],
> };
>
> let {
> 	p: [x, { y }],
> } = obj;
> x; // "Hello"
> y; // "World"
> ```
>
> 注意，这时`p`是模式，不是变量，因此不会被赋值。（对象里的 key）

#### 默认值

> 默认值生效的条件是，对象的属性值严格等于`undefined`。

```javascript
var { x = 3 } = { x: undefined };
x; // 3

var { x = 3 } = { x: null };
x; // null
```

### 字符串的解构赋值

字符串也可以解构赋值。这是因为此时，字符串被转换成了一个类似数组的对象。

```javascript
const [a, b, c, d, e] = 'hello';
a; // "h"
b; // "e"
c; // "l"
d; // "l"
e; // "o"
```

> 类似数组的对象都有一个`length`属性，因此还可以对这个属性解构赋值。
>
> ```javascript
> let { length: len } = 'hello';
> len; // 5
> ```

### 函数参数的解构赋值

函数参数的解构也可以使用默认值。

```javascript
function move({ x = 0, y = 0 } = {}) {
	return [x, y];
}

move({ x: 3, y: 8 }); // [3, 8]
move({ x: 3 }); // [3, 0]
move({}); // [0, 0]
move(); // [0, 0]
```

### 注意

-   已经申明的变量解构赋值

```javascript
// 错误的写法
let x;
{x} = {x: 1};
// SyntaxError: syntax error

// 正确的写法
let x;
({x} = {x: 1});
```

-   由于数组本质是特殊的对象，因此可以对数组进行对象属性的解构。

```javascript
let arr = [1, 2, 3];
let { 0: first, [arr.length - 1]: last } = arr;
first; // 1
last; // 3
```

## 字符串的扩展

### 字符的 Unicode 表示法

```javascript
'\u0061';
// "a"
```

ES6 为字符串添加了遍历器接口，使得字符串可以被`for...of`循环遍历。

```javascript
for (let codePoint of 'foo') {
	console.log(codePoint);
}
// "f"
// "o"
// "o"
```

### 模板字符串

**`${...}`** 大括号内部可以放入任意的 JavaScript 表达式，可以进行运算，以及引用对象属性、嵌套模板字符串

## 函数的扩展

### 箭头函数

> 注意
>
> -   箭头函数没有自己的`this`对象
>
> -   不可以使用`arguments`对象，该对象在函数体内不存在。如果要用，可以用 rest 参数（剩余参数）代替。

> 由于箭头函数使得`this`从“动态”变成“静态”，下面场合不应该使用箭头函数。
>
> -   第一个场合是定义对象的方法，且该方法内部包括`this`。
>
>     ```javascript
>     globalThis.s = 21;
>
>     const obj = {
>     	s: 42,
>     	m: () => console.log(this.s),
>     };
>
>     obj.m(); // 21
>     ```
>
> -   需要动态`this`的时候，也不应使用箭头函数
>
>     ```javascript
>     var button = document.getElementById('press');
>
>     button.addEventListener('click', () => {
>     	this.classList.toggle('on');
>     });
>     ```
>
>     上面代码运行时，点击按钮会报错，因为`button`的监听函数是一个箭头函数，导致里面的`this`就是全局对象。如果改成普通函数，`this`就会动态指向被点击的按钮对象。

## 数组的扩展

### 扩展运算符

#### 复制数组

```javascript
const a1 = [1, 2];
const a2 = a1;

a2[0] = 2;
a1; // [2, 2]
```

#### 合并数组

```javascript
const arr1 = ['a', 'b'];
const arr2 = ['c'];
const arr3 = ['d', 'e'];

// ES5 的合并数组
arr1.concat(arr2, arr3);
// [ 'a', 'b', 'c', 'd', 'e' ]

// ES6 的合并数组
[...arr1, ...arr2, ...arr3];
// [ 'a', 'b', 'c', 'd', 'e' ]

// 不过，这两种方法都是浅拷贝，使用的时候需要注意。
```

#### 字符串

```javascript
[...'hello'];
// [ "h", "e", "l", "l", "o" ]
```

#### 实现了 `Iterator` 接口的对象

```javascript
let nodeList = document.querySelectorAll('div'); // 类数组对象，没有数组的方法属性
let array = [...nodeList]; // 转化为数组
```

#### Map 和 Set 结构，Generator 函数

```javascript
let map = new Map([
	[1, 'one'],
	[2, 'two'],
	[3, 'three'],
]);

let arr = [...map.keys()]; // [1, 2, 3]
```

#### Array.from

> 将类数组对象转化为对象

```javascript
// NodeList对象
let ps = document.querySelectorAll('p');
Array.from(ps).filter(p => {
	return p.textContent.length > 100;
});
9;
// arguments对象
function foo() {
	var args = Array.from(arguments);
	// ...
}

// 只要是部署了 Iterator 接口的数据结构，Array.from都能将其转为数组。
```

## 对象的扩展

### 属性的可枚举性和遍历

#### 可枚举性

```javascript
let obj = { foo: 123 };
Object.getOwnPropertyDescriptor(obj, 'foo');
//  {
//    value: 123,
//    writable: true,
//    enumerable: true,// 可枚举性
//    configurable: true
//  }
```

目前，有四个操作会忽略`enumerable`为`false`的属性。

-   `for...in`循环：只遍历对象自身的和继承的可枚举的属性。
-   `Object.keys()`：返回对象自身的所有可枚举的属性的键名。
-   `JSON.stringify()`：只串行化对象自身的可枚举的属性。
-   `Object.assign()`： 忽略`enumerable`为`false`的属性，只拷贝对象自身的可枚举的属性。

> ES6 规定，所有 Class 的原型的方法都是不可枚举的。

#### 属性的遍历

ES6 一共有 5 种方法可以遍历对象的属性。

##### for...in

循环遍历对象自身的和继承的可枚举属性（不含 Symbol 属性）。

##### Object.keys

返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含 Symbol 属性）的键名。

##### Object.getOwnPropertyNames

返回一个数组，包含对象自身的所有属性（不含 Symbol 属性，但是包括不可枚举属性）的键名。

##### Object.getOwnPropertySymbols

返回一个数组，包含对象自身的所有 Symbol 属性的键名。

##### Reflect.ownKeys

返回一个数组，包含对象自身的（不含继承的）所有键名，不管键名是 Symbol 或字符串，也不管是否可枚举。

---

以上的 5 种方法遍历对象的键名，都遵守同样的属性遍历的次序规则。

1.  首先遍历所有数值键，按照数值升序排列。
2.  其次遍历所有字符串键，按照加入时间升序排列。
3.  最后遍历所有 Symbol 键，按照加入时间升序排列。

```javascript
Reflect.ownKeys({ [Symbol()]: 0, b: 0, 10: 0, 2: 0, a: 0 });
// ['2', '10', 'b', 'a', Symbol()]
```

上面代码中，`Reflect.ownKeys`方法返回一个数组，包含了参数对象的所有属性。这个数组的属性次序是这样的，首先是数值属性`2`和`10`，其次是字符串属性`b`和`a`，最后是 Symbol 属性。

### Super 关键字

`super`，指向当前对象的原型对象。`super`关键字表示原型对象时，只能用在对象的方法之中，用在其他地方都会报错。

## 运算符的扩展

### 指数运算符

`**`

```javascript
2 ** 2; // 4
2 ** 3; // 8
```

### 链判断运算符

**`?.`**

链判断运算符有三种写法

```javascript
obj?.prop; // 对象属性是否存在
obj?.[expr]; // 同上
func?.(...args); // 函数或对象方法是否存在
```

```javascript
const firstName = message?.body?.user?.firstName || 'default';
const fooValue = myForm.querySelector('input[name=foo]')?.value;

const firstName = (message && message.body && message.body.user && message.body.user.firstName) || 'default';
```

### Null 判断运算符

**`??`**

```javascript
const headerText = response.settings.headerText ?? 'Hello, world!';
const animationDuration = response.settings.animationDuration ?? 300;
const showSplashScreen = response.settings.showSplashScreen ?? true;
```

## Set 和 Map 数据结构

### Set

```javascript
const s = new Set();

[2, 3, 5, 4, 5, 2, 2].forEach(x => s.add(x));

for (let i of s) {
	console.log(i);
}
// 2 3 5 4
```

> set 中的值是唯一的

Set 结构的实例有以下属性

-   `Set.prototype.constructor`：构造函数，默认就是`Set`函数。
-   `Set.prototype.size`：返回`Set`实例的成员总数。

Set 实例的方法分为两大类：操作方法和遍历方法

-   `Set.prototype.add(value)`：添加某个值，返回 Set 结构本身。
-   `Set.prototype.delete(value)`：删除某个值，返回一个布尔值，表示删除是否成功。
-   `Set.prototype.has(value)`：返回一个布尔值，表示该值是否为`Set`的成员。
-   `Set.prototype.clear()`：清除所有成员，没有返回值。

Set 结构的实例有四个遍历方法，可以用于遍历成员。

-   `Set.prototype.keys()`：返回键名的遍历器
-   `Set.prototype.values()`：返回键值的遍历器
-   `Set.prototype.entries()`：返回键值对的遍历器
-   `Set.prototype.forEach()`：使用回调函数遍历每个成员

`Array.from`方法可以将 Set 结构转为数组。

```javascript
function dedupe(array) {
	return Array.from(new Set(array));
}

dedupe([1, 1, 2, 3]); // [1, 2, 3]
```

### Map

JavaScript 的对象（Object），本质上是键值对的集合（Hash 结构），但是传统上只能用字符串当作键。这给它的使用带来了很大的限制。

[TODO:](https://es6.ruanyifeng.com/#docs/set-map)

## Class

构造函数的`prototype`属性，在 ES6 的“类”上面继续存在。事实上，类的所有方法都定义在类的`prototype`属性上面。

类的内部所有定义的方法，都是不可枚举的（non-enumerable）

### constructor

`constructor()`方法默认返回实例对象（即`this`），完全可以指定返回另外一个对象

```javascript
class Foo {
	constructor() {
		return Object.create(null);
	}
}

new Foo() instanceof Foo;
// false
```

### getter、setter

存值函数和取值函数是设置在属性的 Descriptor 对象上的。

```javascript
class CustomHTMLElement {
	constructor(element) {
		this.element = element;
	}

	get html() {
		return this.element.innerHTML;
	}

	set html(value) {
		this.element.innerHTML = value;
	}
}

var descriptor = Object.getOwnPropertyDescriptor(CustomHTMLElement.prototype, 'html');

'get' in descriptor; // true
'set' in descriptor; // true
```

### 静态方法

类相当于实例的原型，所有在类中定义的方法，都会被实例继承。

如果在一个方法前，加上`static`关键字，就表示**`该方法不会被实例继承`**，而是直接通过类来调用，这就称为“静态方法”。

```javascript
class Foo {
	static classMethod() {
		return 'hello';
	}
}

Foo.classMethod(); // 'hello'

var foo = new Foo();
foo.classMethod();
// TypeError: foo.classMethod is not a function
```

注意，如果静态方法包含`this`关键字，这个`this`指的是类，而不是实例。

```javascript
class Foo {
	static bar() {
		this.baz();
	}
	static baz() {
		console.log('hello');
	}
	baz() {
		console.log('world');
	}
}

Foo.bar(); // hell
```

### 注意

-   严格模式

类和模块的内部，默认就是严格模式，所以不需要使用`use strict`指定运行模式。只要你的代码写在类或模块之中，就只有严格模式可用。考虑到未来所有的代码，其实都是运行在模块之中，所以 ES6 实际上把整个语言升级到了严格模式。

-   不存在提升

类不存在变量提升（hoist），这一点与 ES5 完全不同。

-   this 的指向

    类的方法内部如果含有`this`，它默认指向类的实例。一旦单独使用该方法，很可能报错。

    ```javascript
    class Logger {
    	printName(name = 'there') {
    		this.print(`Hello ${name}`);
    	}

    	print(text) {
    		console.log(text);
    	}
    }

    const logger = new Logger();
    const { printName } = logger;
    printName(); // TypeError: Cannot read property 'print' of undefined
    ```

    解决方法：

    -   在构造方法中绑定`this`
    -   使用就箭头函数
    -   使用`Proxy`

    ```javascript
    // 在构造方法中绑定this
    class Logger {
    	constructor() {
    		this.printName = this.printName.bind(this);
    	}

    	// ...
    }

    // 使用就箭头函数
    class Obj {
    	constructor() {
    		this.getThis = () => this;
    	}
    }

    const myObj = new Obj();
    myObj.getThis() === myObj; // true

    // 使用Proxy
    function selfish(target) {
    	const cache = new WeakMap();
    	const handler = {
    		get(target, key) {
    			const value = Reflect.get(target, key);
    			if (typeof value !== 'function') {
    				return value;
    			}
    			if (!cache.has(value)) {
    				cache.set(value, value.bind(target));
    			}
    			return cache.get(value);
    		},
    	};
    	const proxy = new Proxy(target, handler);
    	return proxy;
    }

    const logger = selfish(new Logger());
    ```
