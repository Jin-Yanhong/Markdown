## React.Children

### map

### count

### forRach

### only

### toArray

## React.Component

## React.Fragment

## React.PureComponent

## React.cloneElement

## React.createContext

## React.createElement

用于创建虚拟 DOM

## React.createFactory

## React.createRef

## React.forwardRef

## React.isValidElement

## React.lazy

## React.memo

## React.version

# ReactDOM

## ReactDOM.render

渲染虚拟 DOM 到页面

## 创建组件

### 函数时组件

用于简单组件（没有状态)

```javascript
// 创建组件
function test() {
    return <h1>函数式组件</h1>;
}

// 使用组件
ReactDOM.render(<Test />, document.getElementById('#app'));
```

### 创建类式组件

用于创建复杂组件（具有状态)

```javascript
// 创建组件
class Test extends React.Component {
    render() {
        return <h1>函数式组件</h1>;
    }
}

// 使用组件
ReactDOM.render(<Test />, document.getElementById('#app'));
```

### 事件绑定

```javascript
// 创建组件
class Test extends React.Component {
    render() {
        return <h1 onClick={test}>函数式组件</h1>;
    }
}

function test() {
    //
}
```

## 三大核心属性

### state

修改 state 使用 **`setState({key:value})`**，且更新是合并操作

![image-20211130203800257](https://blog-pic-store.oss-cn-beijing.aliyuncs.com/blog/image-20211130203800257.png)

### props

##### 值的传递与接收

![image-20211130204930603](https://blog-pic-store.oss-cn-beijing.aliyuncs.com/blog/image-20211130204930603.png)

#### 展开语法的回顾

![image-20211130205633509](https://blog-pic-store.oss-cn-beijing.aliyuncs.com/blog/image-20211130205633509.png)

#####

![image-20211130210111328](https://blog-pic-store.oss-cn-beijing.aliyuncs.com/blog/image-20211130210111328.png)

mdn

![image-20211130210548482](https://blog-pic-store.oss-cn-beijing.aliyuncs.com/blog/image-20211130210548482.png)

父传子 类型限定，默认值

![image-20211130211344607](https://blog-pic-store.oss-cn-beijing.aliyuncs.com/blog/image-20211130211344607.png)

![image-20211130211803620](https://blog-pic-store.oss-cn-beijing.aliyuncs.com/blog/image-20211130211803620.png)

函数类型为 func

![image-20211130212025364](https://blog-pic-store.oss-cn-beijing.aliyuncs.com/blog/image-20211130212025364.png)

![image-20211130212356440](https://blog-pic-store.oss-cn-beijing.aliyuncs.com/blog/image-20211130212356440.png)

props 限制整理到类的内部

![image-20211130212819893](https://blog-pic-store.oss-cn-beijing.aliyuncs.com/blog/image-20211130212819893.png)



![image-20211130215554766](https://blog-pic-store.oss-cn-beijing.aliyuncs.com/blog/image-20211130215554766.png)

![image-20211130220120634](https://blog-pic-store.oss-cn-beijing.aliyuncs.com/blog/image-20211130220120634.png)

![image-20211130223412814](https://blog-pic-store.oss-cn-beijing.aliyuncs.com/blog/image-20211130223412814.png)



![image-20211130223645124](https://blog-pic-store.oss-cn-beijing.aliyuncs.com/blog/image-20211130223645124.png)

### refs