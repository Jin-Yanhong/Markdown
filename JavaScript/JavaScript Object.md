## Object

### Object.assign(target, ...sources)

> 返回值：目标对象

> `Object.assign` 不会在那些`source`对象值为 [`null`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/null) 或 [`undefined`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined) 的时候抛出错误。

### Object.keys(data)

> 返回值：data 的 key （以数组形式）

```javascript
// 拿到对象的key值索引
for (const key in Object.keys(data)) {
	console.log(key);
}
```

### Object.entries()

> **`Object.entries()`** 方法返回一个给定对象自身可枚举属性的键值对数组，其排列与使用 [`for...in`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...in) 循环遍历该对象时返回的顺序一致（区别在于 for-in 循环还会枚举原型链中的属性）。

```javascript
const object1 = {
    a: 'somestring',s
    b: 42,s
};

for (const [key, value] of Object.entries(object1)) {
    console.log(`${key}: ${value}`);
}

// expected output:
// "a: somestring"
// "b: 42"
```

### Object.freeze()

> 冻结对象详情参考[Object.freeze](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)

### Object.fromEntries()

> Object.fromEntries() 方法把键值对列表转换为一个对象。

```javascript
const entries = new Map([
	['foo', 'bar'],
	['baz', 42],
]);

const obj = Object.fromEntries(entries);

console.log(obj);
// expected output: Object { foo: "bar", baz: 42 }
```

### Object.is()

> `Object.is()` 方法判断两个值是否为[同一个值](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Equality_comparisons_and_sameness)。如果满足以下条件则两个值相等:
>
> -   都是 [`undefined`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined)
> -   都是 [`null`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/null)
> -   都是 `true` 或 `false`
> -   都是相同长度的字符串且相同字符按相同顺序排列
> -   都是相同对象（意味着每个对象有同一个引用）
> -   都是数字且
>     -   都是 `+0`
>     -   都是 `-0`
>     -   都是 [`NaN`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/NaN)
>     -   或都是非零而且非 [`NaN`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/NaN) 且为同一个值

### Object.seal()

> `**Object.seal()**`方法封闭一个对象，阻止添加新属性并将所有现有属性标记为不可配置。当前属性的值只要原来是可写的就可以改变。

```javascript
const object1 = {
	property1: 42,
};

Object.seal(object1);
object1.property1 = 33;
console.log(object1.property1);
// expected output: 33

delete object1.property1; // cannot delete when sealed
console.log(object1.property1);
// expected output: 33
```

## Promise

### Promise.all(iterable)

> 参数：可迭代对象
>
> 注：Array，Map，Set 都属于 ES6 的 iterable 类型

> 返回值：Promise 所有的`Promise`都完成返回完成状态的 Promise，有一个 Promise 为失败，则返回失败状态的 Promise

```javascript
const promise1 = Promise.resolve(3);
const promise2 = 42;
const promise3 = new Promise((resolve, reject) => {
	setTimeout(resolve, 100, 'foo');
});

Promise.all([promise1, promise2, promise3]).then(values => {
	console.log(values);
});
// expected output: Array [3, 42, "foo"]
```

### async、await

> async 函数是使用 async 关键字声明的函数。 async 函数是 AsyncFunction 构造函数的实例， 并且其中允许使用 await 关键字。async 和 await 关键字让我们可以用一种更简洁的方式写出基于 Promise 的异步行为，而无需刻意地链式调用 promise。

```javascript
function resolveAfter2Seconds() {
	return new Promise(resolve => {
		setTimeout(() => {
			resolve('resolved');
		}, 2000);
	});
}

async function asyncCall() {
	console.log('calling');
	const result = await resolveAfter2Seconds();
	console.log(result);
	// expected output: "resolved"
}

asyncCall();
```

### Promise.allSettled()

> 该 **`Promise.allSettled()`** 方法返回一个在所有给定的 promise 都已经`fulfilled`或`rejected`后的 promise，并带有一个对象数组，每个对象表示对应的 promise 结果。
>
> 当您有多个彼此不依赖的异步任务成功完成时，或者您总是想知道每个`promise`的结果时，通常使用它。
>
> 相比之下，`Promise.all()` 更适合彼此相互依赖或者在其中任何一个`reject`时立即结束。

```javascript
const promise1 = Promise.resolve(3);
const promise2 = new Promise((resolve, reject) => setTimeout(reject, 100, 'foo'));
const promises = [promise1, promise2];

Promise.allSettled(promises).then(results => results.forEach(result => console.log(result.status)));

// expected output:
// "fulfilled"
// "rejected"
```

### Promise.any()

> **`Promise.any()`** 接收一个[`Promise`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)可迭代对象，只要其中的一个 `promise` 成功，就返回那个已经成功的 `promise` 。如果可迭代对象中没有一个 `promise` 成功（即所有的 `promises` 都失败/拒绝），就返回一个失败的 `promise `和[`AggregateError`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/AggregateError)类型的实例，它是 [`Error`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Error) 的一个子类，用于把单一的错误集合在一起。本质上，这个方法和[`Promise.all()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)是相反的。
>
> **这个方法用于返回第一个成功的 `promise` 。只要有一个 `promise` 成功此方法就会终止，它不会等待其他的 `promise` 全部完成。**

### Promise.race()

> **`Promise.race(iterable)`** 方法返回一个 promise，一旦迭代器中的某个 promise 解决或拒绝，返回的 promise 就会解决或拒绝。

```javascript
const promise1 = new Promise((resolve, reject) => {
	setTimeout(resolve, 500, 'one');
});

const promise2 = new Promise((resolve, reject) => {
	setTimeout(resolve, 100, 'two');
});

Promise.race([promise1, promise2]).then(value => {
	console.log(value);
	// Both resolve, but promise2 is faster
});
// expected output: "two"
```

### Promise.resolve()

> `**Promise.resolve(value)**`方法返回一个以给定值解析后的[`Promise`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) 对象。如果这个值是一个 promise ，那么将返回这个 promise ；如果这个值是 thenable（即带有[`"then" `](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)方法），返回的 promise 会“跟随”这个 thenable 的对象，采用它的最终状态；否则返回的 promise 将以此值完成。此函数将类 promise 对象的多层嵌套展平。

> **警告：**不要在解析为自身的 thenable 上调用`Promise.resolve`。这将导致无限递归，因为它试图展平无限嵌套的 promise。一个例子是将它与 Angular 中的异步管道一起使用。在[此处](https://angular.io/guide/template-syntax#avoid-side-effects)了解更多信息。
>
> 例如下例代码
>
> ```javascript
> let thenable = {
> 	then: (resolve, reject) => {
> 		resolve(thenable);
> 	},
> };
>
> Promise.resolve(thenable); //这会造成一个死循环
> ```

### Promise 链式调用

```javascript
const promise = new Promise((resolve, reject) => {
	setTimeout(resolve, 500, 'one');
});

promise
	.then(res => {
		// ...
		return res;
	})
	.then(res => {
		// ...
		return res;
		// 返回结果处理完以后，依然是一个Promise
	});
```

## Windows

### window.scrollBy

> 滚动指定的距离

```javascript
window.scrollBy({
    top:0, // 纵向滚动
    left:0 // 横向滚动
    behavior: 'smooth',
})

```

### window.scrollTo

> 滚动到某处

```javascript
window.scrollTo({
	top: 0,
	behavior: 'smooth',
});
```

## Document
