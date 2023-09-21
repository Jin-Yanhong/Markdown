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
	let str = url?.split('#')[0] || window.location.href?.split('#')[0]; //取得整个path
	let num = str.indexOf('?');
	if (num !== -1) {
		str = str.substr(num + 1);
		let arr = str.split('&');
		let obj = {};
		for (let i = 0; i < arr.length; i++) {
			num = arr[i].split('=');
			obj[num[0]] = num[1];
		}
		return obj;
	} else {
		return {};
	}
}
```

#### 深拷贝

```javascript
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
```

#### 树形数据处理

##### ListToTree

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

##### TreeToList

###### 方法 一

```javascript
function handleTree(treeList) {
	let level = -1;
	const output = [];
	function treeToList(treeList, output, level) {
		for (let i = 0; i < treeList.length; i++) {
			const tree = treeList[i];
			tree.level = level + 1;
			output.push(tree);
			const child = tree.children;
			if (child instanceof Array && child.length > 0) {
				treeToList(child, output, level + 1);
				delete tree.children;
			}
		}
		return output;
	}
	const result = treeToList(treeList, output, level);
	return result;
}
```

###### 方法 二

```javascript
function tree2List(tree) {
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
			let tips = (checked && checked[collectionLabel]) || 'Error';
			return tips;
		} else {
			console.log('fieldTranslate Error: the type of the first parameter must be array!');
			return '';
		}
	} else {
		console.log('fieldTranslate Error: please check function parameters!');
		return '';
	}
}
```

#### 复制文本到剪切板

```javascript
function copyToClipboard(text) {
	const input = document.createElement('textarea');
	input.style.opacity = 0;
	input.style.position = 'absolute';
	input.style.left = '-100000px';
	document.body.appendChild(input);
	input.value = text;
	input.select();
	input.setSelectionRange(0, text.length);
	try {
		if (document.execCommand('Copy', 'false', null)) {
			//如果复制成功
			$.message('复制成功！');

			document.body.removeChild(input);
		} else {
			//如果复制失败
			$.message({
				message: '复制失败！',
				type: 'info',
			});
		}
	} catch (err) {
		//如果报错
		$.message({
			message: '复制错误！',
			type: 'error',
		});
	}
}
```

#### 防抖节流

##### 防抖

```javascript
function debounce(fn, delay) {
	let timer = null; //借助闭包
	return function () {
		if (timer) {
			clearTimeout(timer);
		}
		timer = setTimeout(fn, delay); // 简化写法
	};
}
```

##### 节流

```javascript
function throttle(fn, delay) {
	let valid = true;
	return function () {
		if (!valid) {
			//休息时间 暂不接客
			return false;
		}
		// 工作时间，执行函数并且在间隔期内把状态位设为无效
		valid = false;
		setTimeout(() => {
			fn();
			valid = true;
		}, delay);
	};
}
```

##### 字符串转对象

```javascript
// 输入 a.b.c => 输出 { a: { b: { c: {} } } }
/**
 *
 * @param {string} input 输入的字符串
 * @param {*} value 最里层key的值
 * @returns {object} 解析后的对象
 */
function str2Obj(input, value = {}) {
	let output = {};
	const keys = input.split('.').reverse();
	for (let i = 0; i < keys.length; i++) {
		const key = keys[i];
		let temp = {};
		temp[key] = i == 0 ? value : output;
		output = temp;
	}
	return output;
}
```

##### 行政区划编码转文字地址

```javascript
// 行政区划 区域码 反查
function returnLabel(collect, input, result = '') {
	let children = {};
	let collectlength = collect.length;
	for (let i = 0; i < input.length; i++) {
		for (let j = 0; j < collectlength; j++) {
			const val = input[i];
			const obj = collect[j];
			if (obj.value == val) {
				children = obj.children ?? null;
				result += obj.label + ' ';
				input = input.slice(1, input.length);
				if (children) {
					return returnLabel(children, input, result);
				} else {
					break;
				}
			}
		}
	}
	return result;
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

```javascript
/**
 *  @param list 需要分组的数据
 *  @param colCount 所有字段一共分为 colCount 列
 *  @param outPut 接收最后的返回值
 */
groupList(list, colCount) {
  let outPut = [];
  let length = list.length; // 总共 91 条数据
  let colLength = Math.ceil(length / colCount); // 每列 23 条数据
  for (let k = 0; k < colCount; k++) {
    outPut.push([]);
  }
  // 数据分组
  for (let i = 0; i < colCount; i++) {
    for (let j = i * colLength; j < (i + 1) * colLength; j++) {
      list[j] && outPut[i].push(list[j]);
    }
  }
  return outPut;
},
```

### js 获取时间戳

```javascript
const timestamp = Date.parse(new Date());
```

```javascript
const timestamp = new Date().valueOf();
```

```javascript
const timestamp=new Date().getTime()；
```

### 获取 iFrame 内部元素

```javascript
const iframe = document.getElementById('iframe');
const h1 = iframe.contentDocument.getElementById('h1');
```
