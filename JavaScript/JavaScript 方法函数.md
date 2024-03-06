## 工具类函数

### 从 HTML 字符中获取内容

```javascript
export function getTextFromHtml(html = '') {
	let regExp = /<(\S*?)[^>]*>.*?|<.*? \/>/g;
	let text = html.replace(regExp, '');
	return text;
}
```

### 从浏览器 URL 获取参数

```javascript
// 从 URL 获取参数
function UrlSearch(url = window.location.href) {
	let str = url.split('#')[0];
	let num = str.indexOf('?');
	if (num !== -1) {
		str = str.substr(num + 1);
		let arr = str.split('&');
		let obj = {};
		for (let i = 0; i < arr.length; i++) {
			num = arr[i].split('=');
			obj[num[0]] = decodeURIComponent(num[1]);
		}
		return obj;
	} else {
		return {};
	}
}
```

### 深拷贝

#### 方法 1

```javascript
function clone(input) {
	if (input instanceof Array) {
		const object = [];
		for (let i = 0; i < input.length; i++) {
			object.push(clone(input[i]));
		}
		return object;
	}
	if (input instanceof Object) {
		const object = {};
		for (let p in input) {
			object[p] = input[p];
		}
		return object;
	}
}
```

#### 方法 2

```javascript
/**
 * @description deepClone sth
 * @param {Object} source
 */
export function deepClone(source) {
	if (!source && typeof source !== 'object') {
		throw new Error('error arguments', 'deepClone');
	}
	const targetObj = source.constructor === Array ? [] : {};
	Object.keys(source).forEach(keys => {
		if (source[keys] && typeof source[keys] === 'object') {
			targetObj[keys] = deepClone(source[keys]);
		} else {
			targetObj[keys] = source[keys];
		}
	});
	return targetObj;
}
```

### 对象深度合并

```javascript
function objectDeepAssign(...param) {
	let result = Object.assign({}, ...param);
	for (let item of param) {
		for (let [key, value] of Object.entries(item)) {
			if (typeof value === 'object') {
				result[key] = objectDeepAssign(result[key], value);
			}
		}
	}
	return result;
}
```

### 树形数据处理

#### ListToTree

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

#### TreeToList

##### 方法 一

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

##### 方法 二

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

### 数据类型判断

```javascript
Object.prototype.toString.call(obj);
// '[object Array]'
// '[object Object]'
// '[object String]'
```

### 字段翻译

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

### 复制文本到剪切板

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

### 防抖节流

#### 防抖

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

#### 节流

```javascript
function throttle(func, delay) {
	let prev = 0;
	return (...args) => {
		let now = new Date().getTime();
		console.log(now - prev, delay);
		if (now - prev > delay) {
			prev = now;
			return func(...args);
		}
	};
}
```

### 字符串转对象

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

### 根据值显示树形数据对应标签

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

### iframe 相关

#### message 事件

```html
<!-- parent.html -->
<iframe src="./frame.html" frameborder="0"></iframe>
<textarea cols="30" rows="10" id="textarea"></textarea>
<script>
	const iframe = document.querySelector('iframe');
	const frameWindow = iframe.contentWindow;
	document.querySelector('#textarea').addEventListener('input', e => {
		const value = e.srcElement.value;
		frameWindow.postMessage(value, '*');
	});
</script>
```

```html
<!-- iframe.html -->
<script>
	window.addEventListener('message', function (event) {
		console.log('Message received from the parent: ' + event.data); // Message received from parent
	});
</script>
```

#### 给 Iframe 写入内容

```vue
<template>
	<div>
		<iframe ref="iframe" class="iframe" frameborder="0" width="100%" :height="frameHeight" />
	</div>
</template>

<script>
export default {
	mounted() {
		const iframe = this.$refs.iframe;
		iframe?.contentDocument.open();
		iframe?.contentDocument.write('<p> this is a text </p>');
		iframe?.contentDocument.close();
	},
};
</script>
```

### 可视区宽高

```javascript
let obj = {
	innerWidth: window.innerWidth,
	innerHeight: window.innerHeight,
};
```

### 处理页码

```javascript
// 分页参数的处理方式
totalPage = (total + pageSize - 1) / pageSize;
```

## 不实用但有趣

### 通过浏览器录屏

```javascript
document.body.addEventListener('click', async function () {
	let stream = await navigator.mediaDevices.getDisplayMedia({ video: true });
	let mime = MediaRecorder.isTypeSupported('video/webm; codecs=vp9') ? 'video/webm; codecs=vp9' : 'video/webm';

	let mediaRecorder = new MediaRecorder(stream, { mimeType: mime });

	let chunks = [];
	mediaRecorder.addEventListener('dataavailable', function (e) {
		chunks.push(e.data);
	});

	mediaRecorder.addEventListener('stop', function () {
		let blob = new Blob(chunks, { type: chunks[0].type });
		let url = URL.createObjectURL(blob);
		let a = document.createElement('a');
		a.href = url;
		a.download = 'video.webm';
		a.click();
	});
	mediaRecorder.start();
});
```
