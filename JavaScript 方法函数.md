## 常用方法函数

#### 处理页码

```javascript
// 分页参数的处理方式
totalPage = (total + pageSize - 1) / pageSize;
```

#### 从浏览器 URL 获取参数

```javascript
// 从 URL 获取参数
function UrlSearch(url) {
    let str = url.split('#')[0] || location.href.split('#')[0]; //取得整个path
    let num = str.indexOf('?');
    if (num !== -1) {
        str = str.substr(num + 1); //取得所有参数   stringvar.substr(start [, length ]
        let arr = str.split('&'); //各个参数放到数组里
        let obj = {};
        for (let i = 0; i < arr.length; i++) {
            num = arr[i].split('=');
            obj[num[0]] = num[1];
        }
        console.log('获取到的参数如下:');
        console.log(obj);
        return obj;
    } else {
        console.log('当前页面没有参数');
        return {}; //返回空对象，不至于出现红色的错误信息！
    }
}
```

#### 树形数据处理

##### List 2 Tree

```javascript
/**
 * @param {string} list - 原一维数组.
 * @param {string} id - 树形数组数据自身的 id.
 * @param {string} parentId - 树形数组数据的父节点 id.
 * @param {string} children - 树形数组数据的子节点 字段.
 */

function list2Tree(list, id, parentId, children) {
    let result = [];

    if (!Array.isArray(list)) {
        console.log('list2Tree Error: typeof list is not array ');
        return result;
    }

    list.forEach(item => {
        delete item.children;
    });

    let map = {};

    list.forEach(item => {
        map[item[id]] = item;
    });

    list.forEach(item => {
        let parent = map[item[parentId]];
        if (parent) {
            (parent[children] || (parent[children] = [])).push(item);
        } else {
            result.push(item);
        }
    });

    return result;
}
```

##### Tree 2 List

###### 方法 一

```javascript
/****************** 数组\对象 深拷贝 **********************/
//
//
function deepCopy(obj) {
    // 深度复制数组
    if (Object.prototype.toString.call(obj) === '[object Array]') {
        const object = [];
        for (let i = 0; i < obj.length; i++) {
            object.push(deepCopy(obj[i]));
        }
        return object;
    }
    // 深度复制对象
    if (Object.prototype.toString.call(obj) === '[object Object]') {
        const object = {};
        for (let p in obj) {
            object[p] = obj[p];
        }
        return object;
    }
}
/******************** 树形结构转化为一维数组 ****************************/

// 将treeObj中的所有对象，放入一个数组中，要求某个对象在另一个对象的children时，其parent_id是对应的另一个对象的id
// 其原理实际上是数据结构中的广度优先遍历

function tree2Array(treeObj, rootid) {
    const temp = []; // 设置临时数组，用来存放队列
    const out = []; // 设置输出数组，用来存放要输出的一维数组
    temp.push(treeObj);
    // 首先把根元素存放入out中
    let pid = rootid;
    const obj = deepCopy(treeObj);
    obj.pid = pid;
    delete obj['children'];
    out.push(obj);
    // 对树对象进行广度优先的遍历
    while (temp.length > 0) {
        const first = temp.shift();
        const children = first.children;
        if (children && children.length > 0) {
            pid = first.id;
            const len = first.children.length;
            for (let i = 0; i < len; i++) {
                temp.push(children[i]);
                const obj = deepCopy(children[i]);
                obj.pid = pid;
                delete obj['children'];
                out.push(obj);
            }
        }
    }
    return out;
}
```

###### 方法 二

```javascript
function tree2List() {
    var queen = [];
    var out = [];
    queen = queen.concat(tree);
    while (queen.length) {
        var first = queen.shift();
        if (first.children) {
            queen = queen.concat(first.children);
            delete first['children'];
        }

        out.push(first);
    }
    return out;
}
```

#### 数据类型判断

```javascript
Object.prototype.toString.call(obj);
// '[object Array]'
// '[object Object]'
// '[object String]'
```

#### 字段翻译

```javascript
/**
 *
 * @param {*} collection 翻译需要对照的数据
 * @param {*} value 待翻译的值
 * @param {*} collectionField 对照集合中的字段 默认 'value'
 * @param {*} collectionLabel 对照集合中的字段名称 默认 'label'
 * @returns
 */
function fieldTranslate(collection, value, collectionField = 'value', collectionLabel = 'label') {
    if (collection && value && toString(value).length) {
        if (Object.prototype.toString.call(collection) === '[object Array]') {
            let checked = collection.find(ele => {
                return ele[collectionField] == value;
            });
            let tips = (checked && checked[collectionLabel]) || 'Field Translate：未知的数据值,请联系管理员';
            return tips;
        } else {
            console.error('Field Translate Error：类型必须为 Array');
            return '';
        }
    } else {
        console.error('Field Translate Error：数据字段集合、为必须参数!');
        return '';
    }
}
```

#### 复制文本到剪切板

```javascript
function copyToClipboard(text) {
    const input = document.createElement("input");
    input.style.opacity = 0;
    input.style.position = "absolute";
    input.style.left = "-100000px";
    document.body.appendChild(input);
    input.value = text;
    input.select();
    input.setSelectionRange(0, text.length);
    try {
        if (document.execCommand("Copy", "false", null)) {
            //如果复制成功
            $.message("复制成功！");

            document.body.removeChild(input);
        } else {
            //如果复制失败
            $.message({
                message: "复制失败！",
                type: "info"
            });
        }
    } catch (err) {
        //如果报错
        $.message({
            message: "复制错误！",
            type: "error"
        });
    }
}
```



## 项目小结

#### window.postMessage

```javascript
//  外层获取内层
iframe.contentWindow; //获取iframe的window对象；
iframe.contentDocument; //获取iframe的document对象

// 内层获取外层
window.parent;
```

### 可视区宽高

```javascript
let obj = {
    innerWidth: window.innerWidth,
    innerHeight: window.innerHeight,
};
```

#### 几种常见的循环、迭代

```javascript
// 拿到对象的key值索引
for (const key in Object.keys(data)) {
    console.log(key);
}
```

#### window.onbeforeunload

> 页面刷新之前执行的回调

#### JavaScript 随机数

```javascript
parseInt(Math.random() * (max - min + 1) + min, 10);
Math.floor(Math.random() * (max - min + 1) + min); //  Math.floor() 向下取整
```

#### 获取一段时间的起止时间戳

```javascript
getTimestamp(interval = "1hour") {
    /**
     * 以数组形式接受 自定义时间段
     * 其中第一项 是开始时间，第二个是结束时间
     * eg. [ "2022-03-08T16:00:00.000Z", "2022-04-21T16:00:00.000Z" ]
     */
    let time = {};
    let nowMS = new Date().getTime() / 1000; //秒级时间戳
    let timeNow = nowMS;
    let timeBefore;
    let hours = 3600;
    let days = hours * 24;
    let weeks = days * 7;
    let months = days * 30;
    let years = months * 12;

    switch (interval) {
        case "1hour":
            timeBefore = nowMS - hours;
            break;
        case "2hour":
            timeBefore = nowMS - hours * 2;
            break;
        case "4hour":
            timeBefore = nowMS - hours * 4;
            break;
        case "12hour":
            timeBefore = nowMS - hours * 12;
            break;
        case "24hour":
            timeBefore = nowMS - days;
            break;
        case "1week":
            timeBefore = nowMS - weeks;
            break;
        case "1month":
            timeBefore = nowMS - months;
            break;
        case "1year":
            timeBefore = nowMS - years;
            break;
        default:
            timeBefore = Date.parse(interval[0]) / 1000;
            timeNow = Date.parse(interval[1]) / 1000;
            break;
    }
    time.start = parseInt(timeBefore);
    time.end = parseInt(timeNow);
    return time;
}
```
