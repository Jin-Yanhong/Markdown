# 使用场景

饼图图例后显示数据总数、百分比

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

## 自动轮播tiptool

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

tiptool自定义内容

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

