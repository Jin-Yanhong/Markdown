## Array 原生方法

| 方法                                                                       | 语法                                                                              | 描述                                                                                                                                                             |
| -------------------------------------------------------------------------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [concat()](https://www.runoob.com/jsref/jsref-concat-array.html)           | _array1_.concat(_array2_,_array3_,...,_arrayX_)                                   | 连接两个或更多的数组，并返回结果。**不会改变现有的数组，而仅仅会返回被连接数组的一个副本**                                                                       |
| [copyWithin()](https://www.runoob.com/jsref/jsref-copywithin.html)         | array.copyWithin(target, start, end)                                              | 从数组的指定位置拷贝元素到数组的另一个指定位置中。**会改变原数组**                                                                                               |
| [entries()](https://www.runoob.com/jsref/jsref-entries.html)               | array.entries()                                                                   | 返回一个数组的迭代对象，该对象包含数组的键值对 key，value。                                                                                                      |
| [every()](https://www.runoob.com/jsref/jsref-every.html)                   | array.every(function(currentValue,index,arr), thisValue)                          | 方法使用指定函数检测数组中的所有元素：如果数组中检测到有一个元素不满足，则整个表达式返回 false 且剩余的元素不会再进行检测。如果所有元素都满足条件，则返回 true。 |
| [fill()](https://www.runoob.com/jsref/jsref-fill.html)                     | array.fill(value, start, end)                                                     | 使用一个固定值来填充数组。**原数组长度不变，数组改变**                                                                                                           |
| [filter()](https://www.runoob.com/jsref/jsref-filter.html)                 | array.filter(function(currentValue,index,arr), thisValue)                         | 检测数值元素，并返回符合条件所有元素的数组。                                                                                                                     |
| [find()](https://www.runoob.com/jsref/jsref-find.html)                     | array.find(function(currentValue, index, arr),thisValue)                          | 返回符合传入测试（函数）条件的**第一个**数组元素。空数组不会执行                                                                                                 |
| [findIndex()](https://www.runoob.com/jsref/jsref-findindex.html)           | array.findIndex(function(currentValue, index, arr), thisValue)                    | 返回符合传入测试（函数）条件的**第一个**数组元素索引。空数组不会执行                                                                                             |
| [forEach()](https://www.runoob.com/jsref/jsref-foreach.html)               | array.forEach(function(currentValue, index, arr), thisValue)                      | 数组每个元素都执行一次回调函数。空数组不会执行                                                                                                                   |
| [from()](https://www.runoob.com/jsref/jsref-from.html)                     | Array.from(object, mapFunction, thisValue)                                        | 通过给定的对象中创建一个数组。                                                                                                                                   |
| [includes()](https://www.runoob.com/jsref/jsref-includes.html)             | arr.includes(searchElement) arr.includes(searchElement, fromIndex)                | 判断一个数组是否包含一个指定的值。                                                                                                                               |
| [indexOf()](https://www.runoob.com/jsref/jsref-indexof-array.html)         | _array_.indexOf(_item_,_start_)                                                   | 搜索数组中的元素，并返回它所在的位置。                                                                                                                           |
| [isArray()](https://www.runoob.com/jsref/jsref-isarray.html)               | Array.isArray(obj)                                                                | **判断对象是否为数组。**                                                                                                                                         |
| [join()](https://www.runoob.com/jsref/jsref-join.html)                     | _array_.join(_separator_)                                                         | 把数组的所有元素放入一个字符串。**数组转化字符串**                                                                                                               |
| [keys()](https://www.runoob.com/jsref/jsref-keys.html)                     | array.keys()                                                                      | 返回数组的可迭代对象，包含原始数组的键(key)。                                                                                                                    |
| [lastIndexOf()](https://www.runoob.com/jsref/jsref-lastindexof-array.html) | _array_.lastIndexOf(_item_,_start_)                                               | 搜索数组中的元素，并返回它最后出现的位置。从后往前查找                                                                                                           |
| [map()](https://www.runoob.com/jsref/jsref-map.html)                       | array.map(function(currentValue,index,arr), thisValue)                            | 通过指定函数处理数组的每个元素，并返回处理后的数组。**不改变原数组**                                                                                             |
| [pop()](https://www.runoob.com/jsref/jsref-pop.html)                       | _array_.pop()                                                                     | **删除数组的最后一个元素并返回删除的元素，改变原数组**。                                                                                                         |
| [push()](https://www.runoob.com/jsref/jsref-push.html)                     | _array_.push(_item1_, _item2_, ..., _itemX_)                                      | 向数组的末尾添加一个或更多元素，**并返回新的长度**。                                                                                                             |
| [reduce()](https://www.runoob.com/jsref/jsref-reduce.html)                 | array.reduce(function(total, currentValue, currentIndex, arr), initialValue)      | 将数组元素计算为一个值（从左到右）。                                                                                                                             |
| [reduceRight()](https://www.runoob.com/jsref/jsref-reduceright.html)       | array.reduceRight(function(total, currentValue, currentIndex, arr), initialValue) | 将数组元素计算为一个值（从右到左）。                                                                                                                             |
| [reverse()](https://www.runoob.com/jsref/jsref-reverse.html)               | _array_.reverse()                                                                 | **反转数组的元素顺序。**                                                                                                                                         |
| [shift()](https://www.runoob.com/jsref/jsref-shift.html)                   | _array_.shift()                                                                   | **删除并返回数组的第一个元素。改变原数组** **pop**                                                                                                               |
| [slice()](https://www.runoob.com/jsref/jsref-slice-array.html)             | _array_.slice(_start_, _end_)                                                     | 选取数组的一部分，并返回一个新数组。**不该变原数组**，当索引值为负时，从栈尾向栈顶读取                                                                           |
| [some()](https://www.runoob.com/jsref/jsref-some.html)                     | array.some(function(currentValue,index,arr),thisValue)                            | 检测数组元素中是否有元素符合指定条件。如果有一个元素满足条件，则表达式返回*true* , 剩余的元素不会再执行检测，如果没有满足条件的元素，则返回 false                |
| [sort()](https://www.runoob.com/jsref/jsref-sort.html)                     | _array_.sort(_sortfunction_)                                                      | 对数组的元素进行排序。排序顺序可以是字母或数字，并按升序或降序。当数字是按字母顺序排列时"40"将排在"5"前面**改变原数组**                                          |
| [splice()](https://www.runoob.com/jsref/jsref-splice.html)                 | _array_.splice(_index_,_howmany_,_item1_,.....,_itemX_)                           | **`splice() 方法用于添加或删除数组中的元素。这种方法会改变原始数组。`**                                                                                          |
| [toString()](https://www.runoob.com/jsref/jsref-tostring-array.html)       | _array_.toString()                                                                | 把数组转换为字符串，并返回结果。                                                                                                                                 |
| [unshift()](https://www.runoob.com/jsref/jsref-unshift.html)               | _array_.unshift(_item1_,_item2_, ..., _itemX_)                                    | 向数组的**开头添加**一个或更多元素，并返回新的长度。                                                                                                             |
| [valueOf()](https://www.runoob.com/jsref/jsref-valueof-array.html)         | _array_.valueOf()                                                                 | 返回数组对象的原始值。                                                                                                                                           |

### 易混记忆

<table>
    <tr>
        <td>push 结尾添加</td>
        <td>unshift 开头添加</td>
    </tr>
    <tr>
        <td>pop 结尾删除</td>
        <td>shift 开头删除</td>
    </tr>
</table>
## 数组处理

-   ### 数组去重
    -   ES6 数组 set 方法 （ES6 推荐）

```javascript
function unique(arr) {
    return Array.from(new Set(arr));
}
var arr = [1, 1, 'true', 'true', true, true, 15, 15, false, false, 'NaN', 0, 0, 'a', 'a', {}, {}];
console.log(unique(arr));
//[1, "true", true, 15, false, undefined, null, NaN, "NaN", 0, "a", {}, {}]
```

-   -   ES5 splice 循环遍历（ES5 推荐）

```javascript

```
