# 使用场景

## 饼图图例后显示数据总数、百分比

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

## 自动轮播 tiptool

```javascript
function tooltipHighlight(echart, option, need_scroll = false, scroll_count = 1) {
    tooltip_immediately_show(echart, option);

    // 参数检查
    if (!(echart && option)) {
        console.error('echarts自动显示tooltips方法出错，echart、option 参数错误，请检查相关参数！');
        return;
    }

    let dataLength;

    // 数据长度检查
    if (option.series[0] && option.series[0].data) {
        dataLength = option.series[0].data.length;
    } else if (option.dataset && option.dataset.source) {
        dataLength = option.dataset.source.length - 1;
    } else if (dataLength == 0) {
        console.error('当前图表数据配置项暂无数据！');
        return;
    }
    // 当前显示项索引
    let curIndex = 0;
    // 显示周期
    const interval = 3000;

    let zoom_step = 100 / scroll_count;

    // 是否需要滚动，默认不需要滚动
    if (need_scroll) {
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
            // console.log('当前位置', startPage, '当前index', curIndex, '当前页范围', scroll_index_arr[startPage - 1], '起始值', startValue, '结束值', endValue);
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

function tooltip_immediately_show(echart, option) {
    // 统一配置 柱状图 的tooltip 样式
    option.tooltip = {
        trigger: 'axis',
        axisPointer: {
            type: 'shadow',
            shadowStyle: {
                color: 'rgba(150,150,150,0.3)',
            },
        },
        backgroundColor: 'rgba(0,0,0,0.4)',
        borderWidth: 0,
        textStyle: {
            color: 'rgba(255,255,255,0.7)',
        },
        show: true,
    };
    echart.setOption(option);

    // 第一个弹窗默认显示
    echart.dispatchAction({
        type: 'highlight',
        seriesIndex: 0,
        dataIndex: 0,
    });

    // 显示 tooltip
    echart.dispatchAction({
        type: 'showTip',
        seriesIndex: 0,
        dataIndex: 0,
    });
}
```

tiptool 自定义内容

```javascript
function universal_tooltip_formatter(params, your_unit = '') {
    let content = '';
    let str = '';
    if (params instanceof Array) {
        // 数组

        params.map(ele => {
            str = '';
            if (ele.seriesType == 'bar') {
                // 柱状图
                content += `${ele.marker} ${ele.seriesName.includes('series') ? '' : ele.seriesName} ${ele.value} ${your_unit}<br/>`;
                str = str.concat(`${params[0].name ? params[0].name : ''} <br/>` + content);
            } else if (ele.seriesType == 'pie') {
                // 环形图
                // content += `${ele.marker} ${ele.seriesName.includes('series') ? '' : ele.seriesName} ${ele.value} ${your_unit}<br/>`;
                console.log('数组环形图');
            }
        });
    } else if (params instanceof Object) {
        // 对象;
        if (params.seriesType == 'bar') {
            // 柱状图
            content += `${params.marker} ${params.seriesName.includes('series') ? '' : params.seriesName} ${params.value} ${your_unit}<br/>`;
            str = str.concat(`${params.name ? params.name : ''} <br/>` + content);
        }
        if (params.seriesType == 'pie') {
            // 环形图
            content += `${params.marker} ${params.value} ${your_unit} ${params.percent}% <br/>`;
            str = str.concat(`${params.data.name ? params.data.name : ''} <br/>` + content);
        }
    }
    return str;
}
```

## 图表样式相关配置项

```javascript
Option: {
    tooltip: {
        trigger: 'axis',
        axisPointer: {
            // 坐标轴指示器，坐标轴触发有效
            type: 'shadow', // 默认为直线，可选为：'line' | 'shadow' | 'none'
        },
        formatter: '{b0}<br>人口总数:{c1}人<br>常住人口:{c0}人<br>流动人口:{c2}人',
    },
    legend: {
        orient: 'horizontal',
        right: 0,
        itemGap: 20,
        left: 'center',
        textStyle: {
            color: '#ffffff',
        },
        data: ['人口总数', '常住人口', '流动人口'],
    },
    grid: {
        left: 20,
        right: 20,
        top: 20,
        bottom: 0,
        containLabel: true,
    },
    xAxis: {
        type: 'category',
        data: ['网格1', '网格2', '网格3', '网格4', '网格5', '网格6'],
        boundaryGap: ['20%', '20%'],
        axisTick: {
            alignWithLabel: true,
        },
        nameRotate: 45,
        axisLabel: {
            interval: 0, //强制文字产生间隔
            // rotate: '45', //旋转角度
        },
        axisLine: {
            show: true,
            lineStyle: {
                color: '#ffffff',
            },
        },
    },
    yAxis: [
        {
            type: 'value',
            show: true,
            splitLine: {
                show: false,
            },
        },
    ],
    series: [
        {
            type: 'bar',
            barWidth: 12,
            color: '#4dd2ff',
            data: [12504, 20498, 10916, 6637, 16603, 31352],
            itemStyle: {
                normal: {
                    shadowBlur: 10, //发光范围
                    shadowColor: '#0681c8', //发光颜色
                    color: new echarts.graphic.LinearGradient(0, 1, 0, 0, [
                        {
                            offset: 0,
                            color: '#092ff266', // 鼠标指示时，提示框内图例的颜色
                        },
                        {
                            offset: 1,
                            color: '#05eaff',
                        },
                    ]),
                },
            },
        },
    ],
},
```

# Echarts常用API（echarts和echartsInstance） 

## 一、echarts上的方法

一般在项目中引入echarts之后，可以获得一个全局的echarts对象。

##### echarts.init()

创建一个echarts实例，返回echarts实例。不能在单个容器中创建多个echarts实例。

```
(dom: HTMLDivElement|HTMLCanvasElement, theme?: Object|string, opts?: {
    devicePixelRatio?: number
    renderer?: string
    width?: number|string
    height? number|string
}) => ECharts
```

##### echarts.dispose(target: ECharts|HTMLDivElement|HTMLCanvasElement)

销毁实例。实例销毁后无法再被使用。

##### echarts.getInstanceByDom(target: HTMLDivElement|HTMLCanvasElement)

获取Dom容器上的实例。

##### echarts.registerTheme(themeName: string, theme: Object)

注册主题，用于初始化实例的时候指定。

### 2.然后是几个比较具体的方法

##### echarts.connect(group:string|Array)

多个图表实例实现联动

##### echarts.disconnect(group:string)

解除图表实例的联动，如果只需要移除单个实例，可以通过将该图表实例group设为空。

##### echarts.registerMap(mapName: string, geoJson: Object, specialAreas?: Object)

注册可用的地图。必须在包括geo组件或者map图表类型的时候才能使用。

### echarts.getMap(mapName: string) => Object

获取已注册的地图，返回的对象类型是：

```
{
    // 地图的 geoJson 数据
    geoJson: Object,
    // 地图的特殊区域，见 registerMap
    specialAreas: Object
}
```

### echarts.graphic

图形相关帮助方法。主要有两个方法：clipPointsByRect()和clipRectByRect()。
1）clipPointsByRect()
输入一组点，一个矩形，返回被矩形截取过的点

```
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

2）clipRectByRect()
输入两个矩形，返回第二个矩形截取第一个矩形的结果。

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

如果矩形完全被截取完，则会返回undefined。

## 二、echartsInstance的方法

### 1.echartsInstance.group

图表的分组，用于联动。

### 2.echartsInstance.setOption()

```javascript
(option: Object, notMerge?: boolean, lazyUpdate?: boolean)
or
(option: Object, opts?: Object)
```

设置图表实例的配置项和数据，万能接口，所有参数和数据的修改都可以通过setOption来完成。Echarts会合并新的参数和数据，然后刷新图表。还有开启动画的话，Echarts会找到两组数据的差异然后通过合适的动画去展示。
notMerge: 可选参数，是否可以不和之前的option进行合并，默认为false，进行合并。
lazyUpdate：也是一个可选参数，在设置完option之后是否不更新图表。默认为false，即立即更新。
**注意**：lazyUpdate这个参数，设置为false的时候，会立即更新图表。一般在做项目的时候，会根据一定的不同条件值（时间等condition）来在一个div容器上渲染具有不同数据的图表。这时候会从后端获取不同的数据来渲染echarts图表。这时候需要将lazyUpdate参数设置为true，然后图表才能随着数据的变化而正常变化。

### 3.下面是几个获取条件的方法

### 1）echartsInstance.getWidth() => number

获取实例所在容器的宽度。

### 2）echartsInstance.getHeight() => number

获取实例所在容器的高度。

### 3）echartsInstance.getDom() => HTMLCanvasElement|HTMLDivElement

获取实例容器的dom节点

### 4）echartsInstance.getOption() => Object

获取当前实例维护的option对象，返回的option对象是经过用户多次setOption之后修改合并之后的配置项和数据，也记录了用户的交互状态。

### 4.下面是几个和echarts实例事件相关的方法

### 1）echartsInstance.dispatchAction(payload：Object)

触发图表行为。payload可以通过batch属性同时触发多个行为。

### 2）echartsInstance.on()

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

绑定事件处理函数。
Echarts的事件有两种。一种是鼠标事件。还有一种是通过dispatchAction触发的事件，每个action上都有对应的事件。
**注意**：如果事件是外部dispatchAction触发，并且 action 中有 batch 属性触发批量的行为，则相应的响应事件参数里也会把属性都放在 batch 属性中。？？？

### 3）echartsInstance.off((eventName: string, handler?: Function))

解绑事件处理函数.handler是可选参数，可以传入需要解绑的处理函数，如果不传的话，则解绑事件下所有绑定的处理函数。

### 5.涉及到坐标系上的点的方法

### 1）echartsInstance.convertToPixel()

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

### 2）echartsInstance.convertFromPixel()

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

转换像素坐标值到逻辑坐标系上的点，是convertToPixel的逆运算。

### 3）echartsInstance.containPixel

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

### 6.其他的一些方法

### 1）echartsInstance.showLoading(type?: string, opts?: Object)

显示加载动画效果。可以在加载数据前手动调用该接口显示加载动画，在数据加载完成后调用 hideLoading 隐藏加载动画。

-   type
    可选。加载动画类型。目前只有一种‘default’
-   opts
    可选。加载动画配置项，跟type有关。

### 2）echartsInstance.hideLoading()

隐藏动画加载效果

### 3）echartsInstance.getDataURL()

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

导出图表图片，返回一个base64的URL，可以设置为Image的src。

### 4）echartsInstance.getConnectedDataURL()

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

导出联动的图表图片，返回一个base64的url，可以设置为Image的src。导出图片中每个图表的相对位置跟容器的相对位置有关。

### 5）echartsInstance.appendData()

```javascript
(opts: {
    // 要增加数据的系列序号。
    seriesIndex?: string,
    // 增加的数据。
    data?: Array|TypedArray,
}) => string
```

此接口用于，在大数据量（百万以上）的渲染场景，分片加载数据和增量渲染。在大数据量的场景下（例如地理数的打点），就算数据使用二进制格式，也会有几十或上百兆，在互联网环境下，往往需要分片加载。appendData 接口提供了分片加载后增量渲染的能力，渲染新加入的数据块时不会清除原有已经渲染的部分。
**注意**：

-   现在不支持 系列（series） 使用 dataset 同时使用 appendData，只支持系列使用自己的 series.data 时使用 appendData
-   目前并非所有的图表都支持分片加载时的增量渲染。目前支持的图有：ECharts 基础版本的 散点图（scatter） 和 线图（lines）。ECharts GL 的 散点图（scatterGL）、线图（linesGL） 和 可视化建筑群（polygons3D）

### 6）echartsInstance.clear()

清空当前实例。会移除实例中所有的组件和图表。清空后调用getOption会返回一个{}空对象。

### 7）echartsInstance.isDisposed

当前实例是否已经被释放

### 8）echartsInstance.dispose

销毁实例。实例销毁之后无法再被使用。
