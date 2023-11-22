### 定义 css 关键帧

```css
@keyframes animated_div {
	0% {
		transform: rotate(0deg);
		left: 0px;
	}
	25% {
		transform: rotate(20deg);
		left: 0px;
	}
	50% {
		transform: rotate(0deg);
		left: 500px;
	}
	55% {
		transform: rotate(0deg);
		left: 500px;
	}
	70% {
		transform: rotate(0deg);
		left: 500px;
		background: [[1ec7e6]];
	}
	100% {
		transform: rotate(-360deg);
		left: 0px;
	}
}
/* 动画的调用 */
.div {
	animation: animated_div 3s;
}
```

属性列表如下

| 属性                      | 描述                                                                                   |
| :------------------------ | :------------------------------------------------------------------------------------- |
| @keyframes                | 规定动画。                                                                             |
| animation                 | 所有动画属性的简写属性。                                                               |
| animation-name            | 规定 @keyframes 动画的名称。                                                           |
| animation-duration        | 规定动画完成一个周期所花费的秒或毫秒。默认是 0。                                       |
| animation-timing-function | 规定动画的速度曲线。默认是 "ease"。                                                    |
| animation-fill-mode       | 规定当动画不播放时（当动画完成时,或当动画有一个延迟未开始播放时）,要应用到元素的样式。 |
| animation-delay           | 规定动画何时开始。默认是 0。                                                           |
| animation-iteration-count | 规定动画被播放的次数。默认是 1。                                                       |
| animation-direction       | 规定动画是否在下一周期逆向地播放。默认是 "normal"。                                    |
| animation-play-state      | 规定动画是否正在运行或暂停。默认是 "running"。                                         |

### 路径动画

```css
div {
	/* 只改变运动路径,其他保持一致 */
	offset-path: path('M 0 0 L 100 0 L 200 0 L 300 100 L 400 0 L 500 100 L 600 0 L 700 100 L 800 0');
	animation: move 2000ms infinite alternate linear;
}
@keyframes move {
	0% {
		offset-distance: 0%;
	}
	100% {
		offset-distance: 100%;
	}
}
```

### SVG 矢量动画

[超级强大的 SVG SMIL animation 动画详解](https://www.zhangxinxu.com/wordpress/2014/08/so-powerful-svg-smil-animation/)

[纯 CSS 实现帅气的 SVG 路径描边动画效果](https://www.zhangxinxu.com/wordpress/2014/04/animateion-line-drawing-svg-path-%e5%8a%a8%e7%94%bb-%e8%b7%af%e5%be%84/)
