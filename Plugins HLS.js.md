> hls.js 是一个用于在线播放 hls 视频流媒体的 js 的应用，用于播放视频监控等，类似还有 H5 Stream

## 用法示例

```javascript
// 检查当前浏览器环境是否支持
if (Hls.isSupported()) {
  let hlsObj = new Hls();
  this.video = this.$refs.video;

  // 获取视频播放地址
  let videoSrc = 'http://devimages.apple.com/iphone/samples/bipbop/gear3/prog_index.m3u8';

  // HLS 绑定 Video
  hlsObj.attachMedia(_this.video);

  // 当完成绑定时，加载视频资源
  hlsObj.on(Hls.Events.MEDIA_ATTACHED, function () {
    hlsObj.loadSource(videoSrc);
  });

  // 触发 Hls.Events.MANIFEST_PARSED 后 ， 自动开始播放
  hlsObj.on(Hls.Events.MANIFEST_PARSED, function () {
    // 至此 视频开始 播放，可以在这里添加其他业务逻辑 TODO:
    // 结束 播放时，需要停止 加载视频流
    // this.hlsObj.stopLoad(); // 停止加载 视频流
    // this.hlsObj.destroy(); // 销毁实例
  });

  // 错误处理
  hlsObj.on(Hls.Events.ERROR, function (data) {
    if (data.fatal) {
      switch (data.type) {
        case Hls.ErrorTypes.NETWORK_ERROR:
          alert('播放视频监控失败，网络错误!');
          hlsObj.startLoad();
          break;
        case hlsObj.ErrorTypes.MEDIA_ERROR:
          alert('播放视频监控失败，流媒体错误!');
          hlsObj.recoverMediaError();
          break;
        default:
          hlsObj.destroy();
          alert('视频监控播放失败，请联系系统管理员！');
          break;
      }
    }
  });
} else {
  this.$message.error('您的浏览器不支持监控视频播放,请使用Chrome最新版本!');
}
```
