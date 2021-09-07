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
    let str = url || location.href; //取得整个地址栏
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
            s;
            queen = queen.concat(first.children);
            delete first["children"];
        }

        out.push(first);
    }
    return out;
}

```

#### 数据类型判断

```javascript
Object.prototype.toString.call(obj)
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
function fieldTranslate(
    collection,
    value,
    collectionField = "value",
    collectionLabel = "label"
) {
    if (collection && value && toString(value).length) {
        if (Object.prototype.toString.call(collection) === "[object Array]") {
            let checked = collection.find(ele => {
                return ele[collectionField] == value;
            });
            let tips =
                (checked && checked[collectionLabel]) ||
                "Field Translate：未知的数据值,请联系管理员";
            return tips;
        } else {
            console.error("Field Translate Error：类型必须为 Array");
            return "";
        }
    } else {
        console.error("Field Translate Error：数据字段集合、为必须参数!");
        return "";
    }
}
```

## 项目小结

##### window.postMessage iframe 嵌套传参

```javascript
//  外层获取内层
iframe.contentWindow; //获取iframe的window对象；
iframe.contentDocument; //获取iframe的document对象

// 内层获取外层
window.parent;
```

### 可视区宽高

```javascript
console.log(window.innerWidth, window.innerHeight);
```

#### 几种常见的循环、迭代

```javascript
// 拿到对象的key值索引
for (const key in Object.keys(data)) {
    console.log(key);
}
```

