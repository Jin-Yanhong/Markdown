## Object

### Object.assign(target, ...sources)

> 返回值：目标对象

> `Object.assign` 不会在那些`source`对象值为 [`null`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/null) 或 [`undefined`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined) 的时候抛出错误。

### Object.key(data)

> 返回值：data 的 key （以数组形式）

```javascript
// 拿到对象的key值索引
for (const key in Object.keys(data)) {
    console.log(key);
}
```

## Promise

### Promise.all(iterable)

> 参数：可迭代对象 Array、String

> 返回值：Promise
> 所有的`Promise`都完成返回完成状态的 Promise，有一个 Promise 为失败，则返回失败状态的 Promise

-   async、await

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

## Window

```javascript
// 滚动指定的距离
window.scrollBy({
    top:0, // 纵向滚动
    left:0 // 横向滚动
    behavior: 'smooth',
})

// 滚动到某处
window.scrollTo({
    top: 0,
    behavior: 'smooth',
});
```
