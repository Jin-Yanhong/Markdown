# 使用场景

## 代码片段

#### 饼图图例后显示数据总数、百分比

```javascript
legend: {
    type: 'plain',
    orient: 'horizontal',
    pageIconColor: '#9bb3ff',
    pageIconInactiveColor: '#ccc',
    pageTextStyle: {
        color: '#cce8ff',
    },
    icon: 'circle',
    left: 'center',
    bottom: 0,
    textStyle: {
        color: '#ffffff',
        fontSize: 12,
    },
    formatter: function (name) {
        var data = option.series[0].data;
        var total = 0;
        var tarValue;
        for (var i = 0; i < data.length; i++) {
            total += data[i].value;
            if (data[i].name == name) {
                tarValue = data[i].value;
            }
        }
        var v = tarValue;
        var p = Math.round((tarValue / total) * 100);
        return `${name}  ${v}处 (${p}%)`;
    },
},
```

#### 自动轮播 tiptool

```javascript
/**
 *
 * @param {Object} echart echarts 实例
 * @param {Object} option echarts 配置项
 * @param {Boolean} option 此方法参数，是否需要滚动，默认不需滚动
 * @param {Number} interval 图表高亮轮播切换的周期
 */

function tooltipHighlight(echart, option, need_scroll = false, interval = 2000) {
	// 参数检查
	if (!(echart && option)) {
		console.error('echarts自动显示tooltips方法出错，echart、option 参数错误，请检查相关参数！');
		return;
	}

	let dataLength;
	// 数据长度检查
	if (option.series[0] && option.series[0].data) {
		dataLength = option.series[0].data.length;
	} else if (option.series && option.series.data) {
		dataLength = option.series.data.length;
	} else if (option.dataset && option.dataset.source) {
		dataLength = option.dataset.source.length - 1;
	} else if (dataLength == 0) {
		console.error('当前图表数据配置项暂无数据！');
		return;
	}

	// 当前显示项索引
	let curIndex = 0;
	// 显示周期

	// 是否需要滚动，默认不需要滚动
	if (need_scroll) {
		// scroll_count  所有数据都高亮一次，滚动条一共需要滑动的次数，
		let scroll_count;

		if (Object.prototype.toString.call(option.dataZoom) == '[object Array]') {
			scroll_count = 100 / (option.dataZoom[0].end - option.dataZoom[0].start);
		} else if (Object.prototype.toString.call(option.dataZoom) == '[object Object]') {
			scroll_count = 100 / (option.dataZoom.end - option.dataZoom.start);
		} else {
			console.error('当前图表数据配置项没有配置 dataZoom 属性！');
			return;
		}
		let zoom_step = 100 / scroll_count;

		// 滚动配置参数
		let startValue = 0;
		let endValue;
		let startPage = 1;
		let count = Math.ceil(dataLength / scroll_count);
		// 需要切换滚动的索引值
		let scroll_index_arr = [];
		//
		for (let i = 0; i < dataLength + 1; i++) {
			if (i % count == 1) {
				scroll_index_arr.push(i);
			}
		}

		scroll_index_arr.shift();
		// console.log('滑动索引值', scroll_index_arr);
		// debugger;
		setInterval(() => {
			// dataZoom 伴随滚动
			echart.dispatchAction({
				type: 'dataZoom',
				// 开始位置的百分比，0 - 100
				start: startValue,
				// 结束位置的百分比，0 - 100
				end: endValue,
			});

			// 图表当前项高亮
			echart.dispatchAction({
				type: 'highlight',
				seriesIndex: 0,
				dataIndex: curIndex,
			});

			// 显示 tooltip
			echart.dispatchAction({
				type: 'showTip',
				seriesIndex: 0,
				dataIndex: curIndex,
			});

			// 高亮自运算
			if (curIndex < dataLength - 1) {
				curIndex++;
				// console.log('当前项', curIndex);
			} else {
				curIndex = 0;
			}

			if (curIndex == scroll_index_arr[startPage - 1] - startPage) {
				//
				startPage++;
				// console.log('翻页参数叠加了', startPage);
				if (startPage > scroll_index_arr.length + 1) {
					startPage = 1;
					// console.log('翻页参数重置了', startPage);
				}
			}
			// 设置 滚动条 起始值
			startValue = (startPage - 1) * zoom_step;
			// 设置 滚动条 结束值
			endValue = startValue + zoom_step;
			// 数据重置
			if (curIndex == 0) {
				startPage = 1;
				startValue = 0;
				endValue = startValue + zoom_step;
				// console.log('重置', startPage);
			}
		}, interval);
	} else {
		// debugger;
		// 不需要要滚动
		setInterval(() => {
			// 图表当前项高亮
			echart.dispatchAction({
				type: 'highlight',
				seriesIndex: 0,
				dataIndex: curIndex,
			});

			// 显示 tooltip
			echart.dispatchAction({
				type: 'showTip',
				seriesIndex: 0,
				dataIndex: curIndex,
			});

			// 高亮自运算
			if (curIndex < dataLength - 1) {
				curIndex++;
				// console.log('当前项', curIndex);
			} else {
				curIndex = 0;
			}
			// console.log('当前index', curIndex);
		}, interval);
	}
}
```

# Echarts 常用 API

## echarts 上的方法

在项目中引入 echarts 之后，可以获得一个全局的 echarts 对象。

#### echarts.init()

echarts.init(target: HTMLDivElement , theme: Object)

创建一个 echarts 实例，返回 echarts 实例。不能在单个容器中创建多个 echarts 实例。

#### echarts.dispose

echarts.dispose(target: ECharts|HTMLDivElement|HTMLCanvasElement)

销毁实例。实例销毁后无法再被使用。

#### echarts.getInstanceByDom

echarts.getInstanceByDom(target: HTMLDivElement|HTMLCanvasElement)

获取 Dom 容器上的实例。

#### echarts.registerTheme

echarts.registerTheme(themeName: string, theme: Object)

注册主题，用于初始化实例的时候指定。

#### echarts.connect

echarts.connect(group:string|Array)

多个图表实例实现联动

#### echarts.disconnect

echarts.disconnect(group:string)

解除图表实例的联动，如果只需要移除单个实例，可以通过将该图表实例 group 设为空。

#### echarts.registerMap

echarts.registerMap(mapName: string, geoJson: Object, specialAreas?: Object)

注册可用的地图。必须在包括 geo 组件或者 map 图表类型的时候才能使用。

#### echarts.getMap

echarts.getMap(mapName: string) => Object

获取已注册的地图，返回的对象类型是：

```javascript
{
    // 地图的 geoJson 数据
    geoJson: Object,
    // 地图的特殊区域，见 registerMap
    specialAreas: Object
}
```

#### echarts.graphic

图形相关帮助方法。主要有两个方法：clipPointsByRect()和 clipRectByRect()。

-   clipPointsByRect() 输入一组点，一个矩形，返回被矩形截取过的点

```javascript
(
    // 要被截取的点列表，如 [[23, 44], [12, 15], ...]。
    points: Array.<Array.<number>>,
    // 用于截取点的矩形。
    rect: {
        x: number,
        y: number,
        width: number,
        height: number
}
) => Array.<Array.<number>> // 截取结果。
```

-   clipRectByRect() 输入两个矩形，返回第二个矩形截取第一个矩形的结果。

```javascript
(
    // 要被截取的矩形。
    targetRect: {
        x: number,
        y: number,
        width: number,
        height: number
    },
    // 用于截取点的矩形。
    rect: {
        x: number,
        y: number,
        width: number,
        height: number
    }
) => { // 截取结果。
    x: number,
    y: number,
    width: number,
    height: number
}
```

如果矩形完全被截取完，则会返回 undefined。

## EchartsInstance （实例对象）方法

#### echartsInstance.group

图表的分组，用于联动。

#### echartsInstance.setOption()

(option: Object, notMerge?: boolean, lazyUpdate?: boolean)或者(option: Object, opts?: Object) 设置图表实例的配置项和数据，万能接口，所有参数和数据的修改都可以通过 setOption 来完成。Echarts 会合并新的参数和数据，然后刷新图表。还有开启动画的话，Echarts 会找到两组数据的差异然后通过合适的动画去展示。 notMerge: 可选参数，是否可以不和之前的 option 进行合并，默认为 false，进行合并。 lazyUpdate：也是一个可选参数，在设置完 option 之后是否不更新图表。默认为 false，即立即更新。 **注意**：lazyUpdate 这个参数，设置为 false 的时候，会立即更新图表。一般在做项目的时候，会根据一定的不同条件值（时间等 condition）来在一个 div 容器上渲染具有不同数据的图表。这时候会从后端获取不同的数据来渲染 echarts 图表。这时候需要将 lazyUpdate 参数设置为 true，然后图表才能随着数据的变化而正常变化。

## 常用的方法

-   echartsInstance.getWidth() => number

获取实例所在容器的宽度。

-   echartsInstance.getHeight() => number

获取实例所在容器的高度。

-   echartsInstance.getDom() => HTMLCanvasElement|HTMLDivElement

获取实例容器的 dom 节点

-   echartsInstance.getOption() => Object

获取当前实例维护的 option 对象，返回的 option 对象是经过用户多次 setOption 之后修改合并之后的配置项和数据，也记录了用户的交互状态。

### echarts 实例事件相关的方法

-   echartsInstance.dispatchAction(payload：Object)

触发图表行为。payload 可以通过 batch 属性同时触发多个行为。

-   echartsInstance.on()

参数列表：

```javascript
(
    eventName: string,
    handler: Function,
    context?: Object
)
(
    eventName: string,
    query: string|Object,
    handler: Function,
    context?: Object
)
```

绑定事件处理函数。 Echarts 的事件有两种。一种是鼠标事件。还有一种是通过 dispatchAction 触发的事件，每个 action 上都有对应的事件。 **注意**：如果事件是外部 dispatchAction 触发，并且 action 中有 batch 属性触发批量的行为，则相应的响应事件参数里也会把属性都放在 batch 属性中。？？？

-   echartsInstance.off((eventName: string, handler?: Function))

解绑事件处理函数.handler 是可选参数，可以传入需要解绑的处理函数，如果不传的话，则解绑事件下所有绑定的处理函数。

### 涉及到坐标系上的点的方法

-   echartsInstance.convertToPixel()

方法的参数列表：

```javascript
(
    // finder 用于指示『使用哪个坐标系进行转换』。
    // 通常地，可以使用 index 或者 id 或者 name 来定位。
    finder: {
        seriesIndex?: number,
        seriesId?: string,
        seriesName?: string,
        geoIndex?: number,
        geoId?: string,
        geoName?: string,
        xAxisIndex?: number,
        xAxisId?: string,
        xAxisName?: string,
        yAxisIndex?: number,
        yAxisId?: string,
        yAxisName?: string,
        gridIndex?: number,
        gridId?: string
        gridName?: string
    },
    // 要被转换的值。
    value: Array|string
    // 转换的结果为像素坐标值，以 echarts 实例的 dom 节点的左上角为坐标 [0, 0] 点。
) => Array|string
```

转换坐标系上的点到像素坐标值

-   echartsInstance.convertFromPixel()

方法列表参数：

```javascript
(
    // finder 用于指示『使用哪个坐标系进行转换』。
    // 通常地，可以使用 index 或者 id 或者 name 来定位。
    finder: {
        seriesIndex?: number,
        seriesId?: string,
        seriesName?: string,
        geoIndex?: number,
        geoId?: string,
        geoName?: string,
        xAxisIndex?: number,
        xAxisId?: string,
        xAxisName?: string,
        yAxisIndex?: number,
        yAxisId?: string,
        yAxisName?: string,
        gridIndex?: number,
        gridId?: string
        gridName?: string
    },
    // 要被转换的值，为像素坐标值，以 echarts 实例的 dom 节点的左上角为坐标 [0, 0] 点。
    value: Array|string
    // 转换的结果，为逻辑坐标值。
) => Array|string
```

转换像素坐标值到逻辑坐标系上的点，是 convertToPixel 的逆运算。

-   echartsInstance.containPixel

方法参数列表

```javascript
(
    // finder 用于指示『在哪个坐标系或者系列上判断』。
    // 通常地，可以使用 index 或者 id 或者 name 来定位。
    finder: {
        seriesIndex?: number,
        seriesId?: string,
        seriesName?: string,
        geoIndex?: number,
        geoId?: string,
        geoName?: string,
        xAxisIndex?: number,
        xAxisId?: string,
        xAxisName?: string,
        yAxisIndex?: number,
        yAxisId?: string,
        yAxisName?: string,
        gridIndex?: number,
        gridId?: string
        gridName?: string
    },
    // 要被判断的点，为像素坐标值，以 echarts 实例的 dom 节点的左上角为坐标 [0, 0] 点。
    value: Array
) => boolean
```

判断指定的点是否在指定的坐标系或系列上。

### 其他方法

-   echartsInstance.showLoading(type?: string, opts?: Object)

```javascript
// type
// 可选。加载动画类型。目前只有一种‘default’

// opts
// 可选。加载动画配置项，跟 type 有关。
```

显示加载动画效果。可以在加载数据前手动调用该接口显示加载动画，在数据加载完成后调用 hideLoading 隐藏加载动画。

-   echartsInstance.hideLoading()

隐藏动画加载效果

-   echartsInstance.getDataURL()

参数列表

```javascript
(opts: {
    // 导出的格式，可选 png, jpeg
    type?: string,
    // 导出的图片分辨率比例，默认为 1。
    pixelRatio?: number,
    // 导出的图片背景色，默认使用 option 里的 backgroundColor
    backgroundColor?: string,
    // 忽略组件的列表，例如要忽略 toolbox 就是 ['toolbox']
    excludeComponents?: Array.<string>
}) => string
```

导出图表图片，返回一个 base64 的 URL，可以设置为 Image 的 src。

-   echartsInstance.getConnectedDataURL()

参数列表格式

```javascript
(opts: {
    // 导出的格式，可选 png, jpeg
    type?: string,
    // 导出的图片分辨率比例，默认为 1。
    pixelRatio?: number,
    // 导出的图片背景色，默认使用 option 里的 backgroundColor
    backgroundColor?: string,
    // 忽略组件的列表，例如要忽略 toolbox 就是 ['toolbox']
    excludeComponents?: Array.<string>
}) => string
```

导出联动的图表图片，返回一个 base64 的 url，可以设置为 Image 的 src。导出图片中每个图表的相对位置跟容器的相对位置有关。

-   echartsInstance.appendData()

```javascript
(opts: {
	// 要增加数据的系列序号。
	seriesIndex?: string,
	// 增加的数据。
	data?: Array | TypedArray,
}) => string;
```

此接口用于，在大数据量（百万以上）的渲染场景，分片加载数据和增量渲染。在大数据量的场景下（例如地理数的打点），就算数据使用二进制格式，也会有几十或上百兆，在互联网环境下，往往需要分片加载。appendData 接口提供了分片加载后增量渲染的能力，渲染新加入的数据块时不会清除原有已经渲染的部分。

> **注意**：
>
> -   现在不支持 系列（series） 使用 dataset 同时使用 appendData，只支持系列使用自己的 series.data 时使用 appendData
> -   目前并非所有的图表都支持分片加载时的增量渲染。目前支持的图有：ECharts 基础版本的 散点图（scatter） 和 线图（lines）。ECharts GL 的 散点图（scatterGL）、线图（linesGL） 和 可视化建筑群（polygons3D）

-   echartsInstance.clear()

清空当前实例。会移除实例中所有的组件和图表。清空后调用 getOption 会返回一个{}空对象。

-   echartsInstance.isDisposed

当前实例是否已经被释放

-   echartsInstance.dispose

销毁实例。实例销毁之后无法再被使用。

## 配置项相关实例

### 立体柱状图

```javascript
xData = ['本年话务总量', '本年人工话务量', '每万客户呼入量'];
yData = [0, 1230, 425];
option = {
	backgroundColor: '#061326',
	grid: {
		top: '25%',
		left: '-5%',
		bottom: '5%',
		right: '5%',
		containLabel: true,
	},
	tooltip: {
		show: true,
	},
	animation: false,
	xAxis: [
		{
			type: 'category',
			data: xData,
			axisTick: {
				alignWithLabel: true,
			},
			nameTextStyle: {
				color: '#82b0ec',
			},
			axisLine: {
				show: false,
				lineStyle: {
					color: '#82b0ec',
				},
			},
			axisLabel: {
				textStyle: {
					color: '#fff',
				},
				margin: 30,
			},
		},
	],
	yAxis: [
		{
			show: false,
			type: 'value',
			axisLabel: {
				textStyle: {
					color: '#fff',
				},
			},
			splitLine: {
				lineStyle: {
					color: '#0c2c5a',
				},
			},
			axisLine: {
				show: false,
			},
		},
	],
	series: [
		{
			name: '',
			type: 'pictorialBar',
			symbolSize: [40, 10],
			symbolOffset: [0, -6], // 上部椭圆
			symbolPosition: 'end',
			z: 12,
			// "barWidth": "0",
			label: {
				normal: {
					show: true,
					position: 'top',
					// "formatter": "{c}%"
					fontSize: 15,
					fontWeight: 'bold',
					color: '#34DCFF',
				},
			},
			color: '#2DB1EF',
			data: yData,
		},
		{
			name: '',
			type: 'pictorialBar',
			symbolSize: [40, 10],
			symbolOffset: [0, 7], // 下部椭圆
			// "barWidth": "20",
			z: 12,
			color: '#2DB1EF',
			data: yData,
		},
		{
			name: '',
			type: 'pictorialBar',
			symbolSize: function (d) {
				return d > 0 ? [50, 15] : [0, 0];
			},
			symbolOffset: [0, 12], // 下部内环
			z: 10,
			itemStyle: {
				normal: {
					color: 'transparent',
					borderColor: '#2EA9E5',
					borderType: 'solid',
					borderWidth: 1,
				},
			},
			data: yData,
		},
		{
			name: '',
			type: 'pictorialBar',
			symbolSize: [70, 20],
			symbolOffset: [0, 18], // 下部外环
			z: 10,
			itemStyle: {
				normal: {
					color: 'transparent',
					borderColor: '#19465D',
					borderType: 'solid',
					borderWidth: 2,
				},
			},
			data: yData,
		},
		{
			type: 'bar',
			//silent: true,
			barWidth: '40',
			barGap: '10%', // Make series be overlap
			barCateGoryGap: '10%',
			itemStyle: {
				normal: {
					color: new echarts.graphic.LinearGradient(0, 0, 0, 0.7, [
						{
							offset: 0,
							color: '#38B2E6',
						},
						{
							offset: 1,
							color: '#0B3147',
						},
					]),
					opacity: 0.8,
				},
			},
			data: yData,
		},
	],
};
```

如图

![image-20211125173422235](https://blog-pic-store.oss-cn-beijing.aliyuncs.com/blog/echarts%E7%AB%8B%E4%BD%93%E5%9C%86%E6%9F%B1.png)

### 多边形柱状图

```javascript
var xData = ['工单', '影响客户'];
var yData1 = [100, 60];
var yData2 = [80, 40];
var path = 'path://M214,1079l8-6h16l8,6-8,6H222Z';
option = {
	backgroundColor: 'BLACK',
	title: {
		text: '本年预安排停电',
		top: 5,
		left: '20%',
		textStyle: {
			fontSize: 18,
			color: '#fff',
		},
	},
	legend: {
		data: ['总数', '未复电数'],
	},
	grid: {
		top: '25%',
		left: '-5%',
		bottom: '10%',
		right: '5%',
		containLabel: true,
	},
	animation: false,
	xAxis: [
		{
			type: 'category',
			data: xData,
			axisTick: {
				show: false,
				alignWithLabel: true,
			},
			nameTextStyle: {
				color: '#fff',
			},
			axisLine: {
				show: false,
				lineStyle: {
					color: '#82b0ec',
				},
			},
			axisLabel: {
				textStyle: {
					color: '#fff',
				},
				margin: 20,
			},
		},
	],
	yAxis: [
		{
			show: false,
			type: 'value',
			axisLabel: {
				textStyle: {
					color: '#fff',
				},
				formatter: '{value}%',
			},
			splitLine: {
				lineStyle: {
					color: '#0c2c5a',
				},
			},
			axisLine: {
				show: false,
			},
		},
	],
	series: [
		{
			type: 'pictorialBar',
			symbol: path,
			symbolSize: [30, 8],
			symbolOffset: [-20, -5],
			symbolPosition: 'end',
			z: 12,
			color: '#68B4FF',
			data: yData1,
		},
		{
			type: 'pictorialBar',
			symbol: path,
			symbolSize: [30, 8],
			symbolOffset: [20, -5],
			symbolPosition: 'end',
			z: 12,
			color: '#FFCE69',
			data: yData2,
		},
		{
			type: 'pictorialBar',
			symbol: path,
			symbolSize: [30, 8],
			symbolOffset: [-20, 5],
			z: 12,
			color: '#68B4FF',
			data: yData1,
		},
		{
			name: '',
			type: 'pictorialBar',
			symbol: path,
			symbolSize: [30, 8],
			symbolOffset: [20, 5],
			color: '#FFCE69',
			z: 12,
			data: yData2,
		},
		{
			type: 'bar',
			itemStyle: {
				normal: {
					opacity: 0.7,
				},
			},
			barWidth: '30',
			color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
				{
					offset: 0,
					color: '#3D83CD',
				},
				{
					offset: 1,
					color: '#0B3147',
				},
			]),
			data: yData1,
		},
		{
			type: 'bar',
			itemStyle: {
				normal: {
					opacity: 0.7,
				},
			},
			barWidth: '30',
			color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
				{
					offset: 0,
					color: '#CC9F49',
				},
				{
					offset: 1,
					color: '#0B3147',
				},
			]),
			data: yData2,
		},
	],
};
```

如图

![image-20211125173711111](https://blog-pic-store.oss-cn-beijing.aliyuncs.com/blog/echart%E5%A4%9A%E8%BE%B9%E5%BD%A2%E6%9F%B1%E7%8A%B6%E5%9B%BE.png)

### 回调函数使用

```javascript
var colors = ['#32DA56', '#e43c59'];
var xData = ['2016-1', '2016-2', '2016-3', '2016-4', '2016-5', '2016-6', '2016-7', '2016-8', '2016-9', '2016-10', '2016-11', '2016-12'];
var yData = [300, 380, 400, 380, 350, 410, 480, 460, 410, 380, 350, 320];
option = {
	// color: colors,
	xAxis: [
		{
			type: 'category',
			axisTick: {
				show: false,
				alignWithLabel: true,
			},
			splitLine: {
				show: true,
			},
			data: xData,
		},
	],
	yAxis: [
		{
			type: 'value',
			axisTick: {
				show: false,
				alignWithLabel: true,
			},
			splitLine: {
				show: true,
			},
		},
	],
	series: [
		{
			type: 'bar',
			symbol: 'none',
			smooth: true,
			data: yData,
			itemStyle: {
				normal: {
					color: function (d) {
						console.log(d);
						return d.value > 400 ? colors[1] : colors[0];
					},
				},
			},
		},
	],
};
```

如图

![image-20211125173923381](https://blog-pic-store.oss-cn-beijing.aliyuncs.com/blog/echarts%20%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0%E4%BD%BF%E7%94%A8.png)
