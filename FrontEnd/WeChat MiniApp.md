## WXSS 样式

### 隐藏微信滚动条

```css
::-webkit-scrollbar {
	display: none;
	width: 0;
	height: 0;
	color: transparent;
}
```

## js 内容

### 富文本

#### 改变富文本的文本样式

```javascript
.replace(/style\s*?=\s*?(['"])[\s\S]*?\1/gi, '')
.replace(/\<img/gi, '<img style="display:block;width:100%;margin:20px auto;"')
.replace(/\<p/gi, '<p class="p_richText"');
```

```css
.p_richText {
	/**/
}
```

### 微信 Api

#### 微信扫一扫

> 微信扫一扫打开携带参数的小程序码

```javascript
// 普通页面  onLoad:
Page({
	onLoad: function (options) {
		if (options.scene) {
			const shopCode = decodeURIComponent(options.scene);
		}
	},
});

//  App.js (待验证)
Page({
	onLoad: function (options) {
		if (options?.query?.scene) {
			const shopCode = decodeURIComponent(options.query.scene);
		}
	},
});
```

#### 强制使用最新版

```javascript
App({
	onLaunch: function (options) {
		this.autoUpdate();
	},
	autoUpdate: function () {
		var self = this;
		// 获取小程序更新机制兼容
		if (wx.canIUse('getUpdateManager')) {
			const updateManager = wx.getUpdateManager();
			updateManager.onCheckForUpdate(function (res) {
				if (res.hasUpdate) {
					wx.showModal({
						title: '更新提示',
						content: '检测到新版本，是否下载新版本并重启小程序？',
						success: function (res) {
							if (res.confirm) {
								self.downLoadAndUpdate(updateManager);
							} else if (res.cancel) {
								wx.showModal({
									title: '温馨提示',
									content: '本次版本更新涉及到新的功能添加，旧版本无法正常访问的',
									showCancel: false,
									confirmText: '确定更新',
									success: function (res) {
										if (res.confirm) {
											//下载新版本，并重新应用
											self.downLoadAndUpdate(updateManager);
										}
									},
								});
							}
						},
					});
				}
			});
		} else {
			wx.showModal({
				title: '提示',
				content: '当前微信版本过低，无法使用该功能，请升级到最新微信版本后重试。',
			});
		}
	},

	downLoadAndUpdate: function (updateManager) {
		var self = this;
		wx.showLoading();
		updateManager.onUpdateReady(function () {
			wx.hideLoading();
			updateManager.applyUpdate();
		});
		updateManager.onUpdateFailed(function () {
			wx.hideLoading();
			// 新的版本下载失败
			wx.showModal({
				title: '已经有新版本了哟~',
				content: '新版本已经上线，请您删除当前小程序，重新搜索打开',
			});
		});
	},
});
```
