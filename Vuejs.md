## Vuejs查漏补缺

### Event

- v-on事件修饰符

```vue
<!-- 点击事件将只会触发一次 -->
<a v-on:click.once="doThis"></a>

<!-- 滚动事件的默认行为 (即滚动行为) 将会立即触发 -->
<!-- 而不会等待 `onScroll` 完成  -->
<!-- 用于前端优化性能 -->
<!-- 这其中包含 `event.preventDefault()` 的情况 -->
<div v-on:scroll.passive="onScroll">...</div>
```

- 按键修饰符

```vue
<input v-on:keyup.enter="submit">
```

### Value

- v-model

> 输入型文本域触发input事件
>
> 选择型表单触发change事件
>
> - 绑定单选复选，值为表单的checked值
> - 绑定下拉选择，值为所选择的option值
> - 原生select支持多选

几个比较有用的修饰符

```vue
<!-- 在“change”时而非“input”时更新 -->
<input v-model.lazy="msg">

<!-- 如果想自动将用户的输入值转为数值类型-->
<input v-model.number="age" type="number">

<!-- 自动过滤用户输入的首尾空白字符-->
<input v-model.trim="msg">
```

- 通过父组件触发子组件的方法

```javascript
// 子组件自定义事件
this.$emit('eventName',params)

// 在父组件中指定子组件的ref属性，父组件通过
this.$ref.name['子组件的方法']

```

