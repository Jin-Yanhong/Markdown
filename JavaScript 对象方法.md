## Object

- Object.assign(target, ...sources)

> 返回值：目标对象

> `Object.assign` 不会在那些`source`对象值为 [`null`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/null) 或 [`undefined`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined) 的时候抛出错误。

## Promise

- Promise.all(iterable)

> 参数：可迭代对象Array、String

> 返回值：Promise
>
> 所有的`Promise`都完成返回完成状态的Promise，有一个Promise为失败，则返回失败状态的Promise