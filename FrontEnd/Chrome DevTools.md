## Source

### Event

监听元素所有的事件

```javascript
monitorEvents($0);
```

## Console

### 变量打印

-   字符 - %s

```javascript
console.log('打印 %s', '1');
```

-   对象 - %o

```javascript
console.log('打印 %o', {});
```

-   数值 - %d

```javascript
console.log('打印 %s', 1);
```

-   样式 - %c

```javascript
console.log('%c 文本1', 'background: #27ae60;color:#ecf0f1;');
```

## Tips

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
