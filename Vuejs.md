# Vuejs 查漏补缺

---

## 原理

> Vue 最独特的特性之一，是其非侵入性的响应式系统。

![data](https://blog-pic-store.oss-cn-beijing.aliyuncs.com/blog/lifecycle.png)

## 动态绑定

### vue 动态引入背景图片

```vue
<div
  :style="{
    backgroundImage: 'url(' + item.imgsrc + ')',
    backgroundSize: '100% 100%',
    backgroundRepeat: 'no-repeat',
  }"
>This is a message</div>
```

## API

### Event

- v-on 事件修饰符

```vue
<!-- 点击事件将只会触发一次 -->
<a v-on:click.once="doThis"></a>
<!-- 滚动事件的默认行为 (即滚动行为) 将会立即触发 -->
<!-- 而不会等待 `onScroll` 完成  -->
<!-- 用于前端优化性能 -->
<!-- 这其中包含 `event.preventDefault()` 的情况 -->
<div v-on:scroll.passive="onScroll">...</div>
.stop - 调用 event.stopPropagation()。 .prevent - 调用 event.preventDefault()。 .capture - 添加事件侦听器时使用 capture 模式。 .self -
只当事件是从侦听器绑定的元素本身触发时才触发回调。 .{keyCode | keyAlias} - 只当事件是从特定键触发时才触发回调。 .native - 监听组件根元素的原生事件。 .once -
只触发一次回调。 .left - (2.2.0) 只当点击鼠标左键时触发。 .right - (2.2.0) 只当点击鼠标右键时触发。 .middle - (2.2.0) 只当点击鼠标中键时触发。 .passive -
(2.3.0) 以 { passive: true } 模式添加侦听器
```

- 按键修饰符

```vue
<input v-on:keyup.enter="submit">
```

### Value

- v-model

> 输入型文本域触发 input 事件
>
> 选择型表单触发 change 事件
>
> - 绑定单选复选，值为表单的 checked 值
> - 绑定下拉选择，值为所选择的 option 值
> - 原生 select 支持多选
>   几个比较有用的修饰符

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
this.$emit('eventName', params);
// 在父组件中指定子组件的ref属性，父组件通过
this.$ref.name['子组件的方法'];
```

### 生命周期钩子函数

- 生命周期图示

<img src="https://gitee.com/Coder-jin/PicStore/raw/master/lifecycle.png" alt="Vue 实例生命周期"  />

示例：

![image-20210408100239292](https://gitee.com/Coder-jin/PicStore/raw/master/image-20210408100239292.png)

#### beforeCreate

> 在实例初始化之后，数据观测 (data observer) 和 event/watcher 事件配置之前被调用。

#### created

> 在实例创建完成后被立即调用。在这一步，实例已完成以下的配置：数据观测 (data observer)，property 和方法的运算，watch/event 事件回调。然而，挂载阶段还没开始，`$el` property 目前尚不可用。

#### beforeMount

> 在挂载开始之前被调用：相关的 `render` 函数首次被调用。
>
> **该钩子在服务器端渲染期间不被调用。**

#### mounted

> 实例被挂载后调用，这时 `el` 被新创建的 `vm.$el` 替换了。如果根实例挂载到了一个文档内的元素上，当 `mounted` 被调用时 `vm.$el` 也在文档内。
>
> 注意 `mounted` **不会**保证所有的子组件也都一起被挂载。如果你希望等到整个视图都渲染完毕，可以在 `mounted` 内部使用 [vm.$nextTick]

```javascript
mounted: function () {
  this.$nextTick(function () {
    // Code that will run only after the
    // entire view has been rendered
  })
}
```

> **该钩子在服务器端渲染期间不被调用。**

#### beforeUpdate

> 数据更新时调用，发生在虚拟 DOM 打补丁之前。这里适合在更新之前访问现有的 DOM，比如手动移除已添加的事件监听器。
>
> **该钩子在服务器端渲染期间不被调用，因为只有初次渲染会在服务端进行**

#### updated

> 由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子。
>
> 当这个钩子被调用时，组件 DOM 已经更新，所以你现在可以执行依赖于 DOM 的操作。然而在大多数情况下，你应该避免在此期间更改状态。如果要相应状态改变，通常最好使用[计算属性](https://cn.vuejs.org/v2/api/#computed)或 [watcher](https://cn.vuejs.org/v2/api/#watch) 取而代之。
>
> 注意 `updated` **不会**保证所有的子组件也都一起被重绘。如果你希望等到整个视图都重绘完毕，可以在 `updated` 里使用 [vm.$nextTick](https://cn.vuejs.org/v2/api/#vm-nextTick)：

```javascript
updated: function () {
  this.$nextTick(function () {
    // Code that will run only after the
    // entire view has been re-rendered
  })
}
```

#### activated

> 被 keep-alive 缓存的组件激活时调用。
>
> **该钩子在服务器端渲染期间不被调用。**

参考

- [构建组件 - keep-alive](https://cn.vuejs.org/v2/api/#keep-alive)
- [动态组件 - keep-alive](https://cn.vuejs.org/v2/guide/components-dynamic-async.html#在动态组件上使用-keep-alive)

#### deactivated

> 被 keep-alive 缓存的组件停用时调用。
>
> **该钩子在服务器端渲染期间不被调用。**

参考

- [构建组件 - keep-alive](https://cn.vuejs.org/v2/api/#keep-alive)
- [动态组件 - keep-alive](https://cn.vuejs.org/v2/guide/components-dynamic-async.html#在动态组件上使用-keep-alive)

#### beforeDestory

> 实例销毁之前调用。在这一步，实例仍然完全可用。
>
> **该钩子在服务器端渲染期间不被调用。**

#### destroyed

> 实例销毁后调用。该钩子被调用后，对应 Vue 实例的所有指令都被解绑，所有的事件监听器被移除，所有的子实例也都被销毁。
>
> **该钩子在服务器端渲染期间不被调用。**

#### [errorCaptured](https://cn.vuejs.org/v2/api/#errorCaptured)

- 类型：(err: Error, vm: Component, info: string) => ?boolean

### 全局 API

#### Vue.extend()

> 使用基础 Vue 构造器，创建一个“子类”。参数是一个包含组件选项的对象。
>
> `data` 选项是特例，需要注意 - 在 `Vue.extend()` 中它必须是函数
>
> 这点类似于 jQuery.extend()

```html
<div id="mount-point"></div>
```

```javascript
// 创建构造器
var Profile = Vue.extend({
  template: '<p>{{firstName}} {{lastName}} aka {{alias}}</p>',
  data: function () {
    return {
      firstName: 'Walter',
      lastName: 'White',
      alias: 'Heisenberg',
    };
  },
});
// 创建 Profile 实例，并挂载到一个元素上。
new Profile().$mount('#mount-point');
```

结果如下

```html
<p>Walter White aka Heisenberg</p>
```

#### Vue.nextTick()

> 在下次 DOM 更新循环结束之后执行延迟回调。在修改数据之后立即使用这个方法，获取更新后的 DOM。

```javascript
// 修改数据
vm.msg = 'Hello';
// DOM 还没有更新
Vue.nextTick(function () {
  // DOM 更新了
});

// 作为一个 Promise 使用 (2.1.0 起新增，详见接下来的提示)
Vue.nextTick().then(function () {
  // DOM 更新了
});
```

> 2.1.0 起新增：如果没有提供回调且在支持 Promise 的环境中，则返回一个 Promise。

#### Vue.set()

> 向响应式对象中添加一个 property，并确保这个新 property 同样是响应式的，且触发视图更新。它必须用于向响应式对象上添加新 property，因为 Vue 无法探测普通的新增 property (比如 `this.myObject.newProperty = 'hi'`)

> 注意对象不能是 Vue 实例，或者 Vue 实例的根数据对象。

#### Vue.filter()

> 注册或获取全局过滤器。

```javascript
// 注册
Vue.filter('my-filter', function (value) {
  // 返回处理后的值
});

// getter，返回已注册的过滤器
var myFilter = Vue.filter('my-filter');
```

#### Vue.use()

> 安装 Vue.js 插件。如果插件是一个对象，必须提供 `install` 方法。如果插件是一个函数，它会被作为 install 方法。install 方法调用时，会将 Vue 作为参数传入。
>
> 该方法需要在调用 `new Vue()` 之前被调用。
>
> 当 install 方法被同一个插件多次调用，插件将只会被安装一次。

#### [Vue.component()](https://cn.vuejs.org/v2/api/#Vue-component)

> 注册或获取全局组件。注册还会自动使用给定的 `id` 设置组件的名称

```javascript
// 注册组件，传入一个扩展过的构造器
Vue.component(
  'my-component',
  Vue.extend({
    /* ... */
  })
);

// 注册组件，传入一个选项对象 (自动调用 Vue.extend)
Vue.component('my-component', {
  /* ... */
});

// 获取注册的组件 (始终返回构造器)
var MyComponent = Vue.component('my-component');
```

#### Vue.directive()

> 注册或获取全局指令

```javascript
// 注册
Vue.directive('my-directive', {
  bind: function () {},
  inserted: function () {},
  update: function () {},
  componentUpdated: function () {},
  unbind: function () {},
});

// 注册 (指令函数)
Vue.directive('my-directive', function () {
  // 这里将会被 `bind` 和 `update` 调用
});

// getter，返回已注册的指令
var myDirective = Vue.directive('my-directive');
```

### Watch

监听路由

##### 方法一

```javascript
//
watch:{
  $route(to,from){
    console.log(to.path);
  }
},
```

##### 方法二

```javascript
//
watch: {
  $route: {
    handler: function(val, oldVal){
      console.log(val);
    },
    // 深度观察监听
    deep: true
  }
},
```

##### 方法三

```javascript
//
watch: {
  '$route':'getPath'
},
methods: {
  getPath(){
    console.log(this.$route.path);
  }
}
```

### 插槽

#### 后备内容

有时为一个插槽设置具体的后备 (也就是默认的) 内容是很有用的，它只会在没有提供内容的时候被渲染。

> 类似于默认值

#### 具名插槽

> 可以用于放置多个插槽

子组件

```vue
<div class="container">
  <header>
    <slot name="header"></slot>
  </header>
  <main>
    <slot></slot>
  </main>
  <footer>
    <slot name="footer"></slot>
  </footer>
</div>
```

父组件

```vue
<base-layout>
  <template v-slot:header>
    <h1>Here might be a page title</h1>
  </template>

  <p>A paragraph for the main content.</p>
  <p>And another one.</p>

  <template v-slot:footer>
    <p>Here's some contact info</p>
  </template>
</base-layout>
```

#### 作用域插槽 子组件使用

> ##### 父组件的数据

为了让 `user` 在父级的插槽内容中可用，我们可以将 `user` 作为 `<slot>` 元素的一个 attribute 绑定上去：

```vue
<span>
  <slot v-bind:user="user">
    {{ user.lastName }}
  </slot>
</span>
```

绑定在 `<slot>` 元素上的 attribute 被称为**插槽 prop**。现在在父级作用域中，我们可以使用带值的 `v-slot` 来定义我们提供的插槽 prop 的名字：

```vue
<current-user>
  <template v-slot:default="slotProps">
    {{ slotProps.user.firstName }}
  </template>
</current-user>
```

在这个例子中，我们选择将包含所有插槽 prop 的对象命名为 `slotProps`，但你也可以使用任意你喜欢的名字。

# 代码片段

### 新标签页打开页面

```javascript
const { href } = this.$router.resolve({
    path: '/跳转的页面路由',
    query: {
        //要传的参数
        id: this.id,
    },
});
window.open(href, '_blank'); //打开新的窗口
```

