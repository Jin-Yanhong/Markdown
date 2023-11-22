## React.Children

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

### props

#### 值的传递

```js

```

#### 值的接收

```jsx
function formatName(user) {
	return user.firstName + ' ' + user.lastName;
}

const user = {
	firstName: 'Harper',
	lastName: 'Perez',
};

const element = <h1>Hello, {formatName(user)}!</h1>;

ReactDOM.render(element, document.getElementById('root'));
```

#### 组件参数选项

函数类型为 func

props 限制整理到类的内部

### refs
