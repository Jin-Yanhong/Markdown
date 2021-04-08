## 常用方法函数

-   ### 处理页码

```javascript
// 分页参数的处理方式
totalPage = (total + pageSize - 1) / pageSize;
```

-   ### 从浏览器 URL 获取参数

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

-   ### 树形数据处理

```javascript
/**
 * 构造树型结构数据
 * @param {*} data 数据源
 * @param {*} id id字段 默认 'id'
 * @param {*} parentId 父节点字段 默认 'parentId'
 * @param {*} children 孩子节点字段 默认 'children'
 * @param {*} rootId 根Id 默认 0
 */
function handleTree(data, id, parentId, children, rootId) {
    id = id || 'id';
    parentId = parentId || 'parentId';
    children = children || 'children';
    rootId =
        rootId ||
        Math.min.apply(
            Math,
            data.map(item => {
                return item[parentId];
            })
        ) ||
        0;
    //对源数据深度克隆
    const cloneData = JSON.parse(JSON.stringify(data));
    //循环所有项
    const treeData = cloneData.filter(father => {
        let branchArr = cloneData.filter(child => {
            //返回每一项的子级数组
            return father[id] === child[parentId];
        });
        branchArr.length > 0 ? (father.children = branchArr) : '';
        //返回第一层
        return father[parentId] === rootId;
    });
    return treeData != '' ? treeData : data;
}
```

## 项目小结

### iframe 嵌套传参

```javascript
iframe.contentWindow; //获取iframe的window对象；
iframe.contentDocument; //获取iframe的document对象
```

### 动态赋值

```javascript
_this.setData({
    ['orderInfo[' + index + '].mwShoppingCartList']: hasEfficacy,
});
```
