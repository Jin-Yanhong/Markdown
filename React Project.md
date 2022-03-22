## 局部样式

### 组件的样式文件

```css
/* components.module.css 文件*/
.title {
    background-color: orange;
}
```

> 注意这里必须是`xxx.module.css`,css 样式模块化

### 父组件引用

```jsx
import React, { Component } from "react";
// 在此处以模块化的方式引入
import hello from "./index.module.css";

export default class Hello extends Component {
    render() {
        // 在此处以模块化的方式使用
        return <h2 className={hello.title}>Hello,React!</h2>;
    }
}
```

## 组件传值

### 父传子

-   子组件

```jsx
export default class Header extends Component {
    //对接收的props进行：类型、必要性的限制
    static propTypes = {
        addTodo: PropTypes.func.isRequired,
    };

    //键盘事件的回调
    handleKeyUp = (event) => {
        //解构赋值获取keyCode,target
        const { keyCode, target } = event;
        //判断是否是回车按键
        if (keyCode !== 13) return;
        //添加的todo名字不能为空
        if (target.value.trim() === "") {
            alert("输入不能为空");
            return;
        }
        //准备好一个todo对象
        const todoObj = { id: nanoid(), name: target.value, done: false };
        //将todoObj传递给App
        this.props.addTodo(todoObj);
        //清空输入
        target.value = "";
    };

    render() {
        return (
            <div className="todo-header">
                <input
                    onKeyUp={this.handleKeyUp}
                    type="text"
                    placeholder="请输入你的任务名称，按回车键确认"
                />
            </div>
        );
    }
}
```

-   父组件

```jsx
export default class App extends Component {
    render() {
        const { todos } = this.state;
        return (
            <div className="todo-container">
                <div className="todo-wrap">
                    <Header addTodo={this.addTodo} />
                </div>
            </div>
        );
    }
}
```

父组件一次性传值

```jsx
<List {...this.state} />
```

### 子传父

-   子组件

-   父组件

## 事件的绑定

```jsx
import React, { Component } from "react";

export default class App extends Component {
    handleEvent() {
        console.log("事件被触发了");
    }

    render() {
        return (
            <div>
                <button onClick={this.handleEvent}>Click me!</button>
            </div>
        );
    }
}
```

## 配置代理

-   方法一

在 **`package.json`** 中追加如下配置

```json
{
    "proxy": "http://localhost:5000"
}
```

-   方法二

1.  第一步：创建代理配置文件

    在 src 下创建配置文件：**`src/setupProxy.js`**

2.  编写 setupProxy.js 配置具体代理规则：

```javascript
const proxy = require("http-proxy-middleware");

module.exports = function (app) {
    app.use(
        proxy("/api1", {
            target: "http://localhost:5000",
            changeOrigin: true,
            pathRewrite: { "^/api1": "" },
        }),
        proxy("/api2", {
            target: "http://localhost:5001",
            changeOrigin: true,
            pathRewrite: { "^/api2": "" },
        })
    );
};
```

> **`说明：`**
> 优点：可以配置多个代理，可以灵活的控制请求是否走代理。
>
> 缺点：配置繁琐，前端请求资源时必须加前缀。

## 路由

### 基本使用

```jsx
import React, { Component } from "react";
import { Link, Route } from "react-router-dom";
import Home from "./components/Home";
import About from "./components/About";

export default class App extends Component {
    render() {
        return (
            <div>
                <div className="row">
                    <div className="col-xs-2 col-xs-offset-2">
                        <div className="list-group">
                            <Link className="list-group-item" to="/about">
                                About
                            </Link>
                            <Link className="list-group-item" to="/home">
                                Home
                            </Link>
                        </div>
                    </div>
                    <div className="col-xs-6">
                        <div className="panel">
                            <div className="panel-body">
                                {/* 注册路由 */}
                                <Route path="/about" component={About} />
                                <Route path="/home" component={Home} />
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        );
    }
}
```

### NavLink 使用

```jsx
import React, { Component } from "react";
import { NavLink, Route } from "react-router-dom";
import Home from "./pages/Home"; //Home是路由组件
import About from "./pages/About"; //About是路由组件
import Header from "./components/Header"; //Header是一般组件

export default class App extends Component {
    render() {
        return (
            <div>
                <div className="row">
                    <div className="col-xs-2 col-xs-offset-2">
                        <div className="list-group">
                            <NavLink
                                activeClassName="atguigu"
                                className="list-group-item"
                                to="/about"
                            >
                                About
                            </NavLink>
                            <NavLink
                                activeClassName="atguigu"
                                className="list-group-item"
                                to="/home"
                            >
                                Home
                            </NavLink>
                        </div>
                    </div>
                    <div className="col-xs-6">
                        <div className="panel">
                            <div className="panel-body">
                                {/* 注册路由 */}
                                <Route path="/about" component={About} />
                                <Route path="/home" component={Home} />
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        );
    }
}
```

### Switch 使用

```jsx
import React, { Component } from "react";
import { Route, Switch } from "react-router-dom";
import Home from "./pages/Home"; //Home是路由组件
import About from "./pages/About"; //About是路由组件
import Header from "./components/Header"; //Header是一般组件
import MyNavLink from "./components/MyNavLink";
import Test from "./pages/Test";

export default class App extends Component {
    render() {
        return (
            <div>
                <div className="row">
                    <div className="col-xs-offset-2 col-xs-8">
                        <Header />
                    </div>
                </div>
                <div className="row">
                    <div className="col-xs-2 col-xs-offset-2">
                        <div className="list-group">
                            <MyNavLink to="/about">About</MyNavLink>
                            <MyNavLink to="/home">Home</MyNavLink>
                        </div>
                    </div>
                    <div className="col-xs-6">
                        <div className="panel">
                            <div className="panel-body">
                                {/* 注册路由 */}
                                <Switch>
                                    <Route path="/about" component={About} />
                                    <Route path="/home" component={Home} />
                                    <Route path="/home" component={Test} />
                                </Switch>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        );
    }
}
```

### Redirect 使用

```jsx
import React, { Component } from "react";
import { Route, Switch, Redirect } from "react-router-dom";
import Home from "./pages/Home"; //Home是路由组件
import About from "./pages/About"; //About是路由组件
import Header from "./components/Header"; //Header是一般组件
import MyNavLink from "./components/MyNavLink";

export default class App extends Component {
    render() {
        return (
            <div>
                <div className="row">
                    <div className="col-xs-2 col-xs-offset-2">
                        <div className="list-group">
                            <MyNavLink to="/about">About</MyNavLink>
                            <MyNavLink to="/home">Home</MyNavLink>
                        </div>
                    </div>
                    <div className="col-xs-6">
                        <div className="panel">
                            <div className="panel-body">
                                {/* 注册路由 */}
                                <Switch>
                                    <Route path="/about" component={About} />
                                    <Route path="/home" component={Home} />
                                    <Redirect to="/about" />
                                </Switch>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        );
    }
}
```

### 精准匹配与模糊匹配

```jsx
import React, { Component } from "react";
import { Route, Switch } from "react-router-dom";
import Home from "./pages/Home"; //Home是路由组件
import About from "./pages/About"; //About是路由组件
import Header from "./components/Header"; //Header是一般组件
import MyNavLink from "./components/MyNavLink";

export default class App extends Component {
    render() {
        return (
            <div>
                <div className="row">
                    <div className="col-xs-offset-2 col-xs-8">
                        <Header />
                    </div>
                </div>
                <div className="row">
                    <div className="col-xs-2 col-xs-offset-2">
                        <div className="list-group">
                            <MyNavLink to="/about">About</MyNavLink>
                            <MyNavLink to="/home/a/b">Home</MyNavLink>
                        </div>
                    </div>
                    <div className="col-xs-6">
                        <div className="panel">
                            <div className="panel-body">
                                <Switch>
                                    <Route
                                        exact
                                        path="/about"
                                        component={About}
                                    />
                                    <Route
                                        exact
                                        path="/home"
                                        component={Home}
                                    />
                                </Switch>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        );
    }
}
```

### 路由嵌套

```jsx

```

## 路由传参

### params 参数

#### 传递

```jsx
import React, { Component } from "react";
import { Link, Route } from "react-router-dom";
import Detail from "./Detail";

export default class Message extends Component {
    render() {
        const { messageArr } = this.state;
        return (
            <div>
                <ul>
                    {messageArr.map((msgObj) => {
                        return (
                            <li key={msgObj.id}>
                                {/* 向路由组件传递params参数 */}
                                <Link
                                    to={`/home/message/detail/${msgObj.id}/${msgObj.title}`}
                                >
                                    {msgObj.title}
                                </Link>
                            </li>
                        );
                    })}
                </ul>
                <hr />
                {/* 声明接收params参数 */}
                <Route
                    path="/home/message/detail/:id/:title"
                    component={Detail}
                />
            </div>
        );
    }
}
```

#### 接收

```jsx
import React, { Component } from "react";

export default class Detail extends Component {
    render() {
        console.log(this.props);
        // 接收params参数
        const { id, title } = this.props.match.params;
    }
}
```

### search 参数

#### 传递

```jsx
import React, { Component } from "react";
import { Link, Route } from "react-router-dom";
import Detail from "./Detail";

export default class Message extends Component {
    render() {
        const { messageArr } = this.state;
        return (
            <div>
                <ul>
                    {messageArr.map((msgObj) => {
                        return (
                            <li key={msgObj.id}>
                                {/* 向路由组件传递search参数 */}
                                <Link
                                    to={`/home/message/detail/?id=${msgObj.id}&title=${msgObj.title}`}
                                >
                                    {msgObj.title}
                                </Link>
                            </li>
                        );
                    })}
                </ul>
                <hr />
                {/* search参数无需声明接收，正常注册路由即可 */}
                <Route path="/home/message/detail" component={Detail} />
            </div>
        );
    }
}
```

#### 接收

```jsx

```

### state 参数

#### 传递

```jsx
import React, { Component } from "react";
import { Link, Route } from "react-router-dom";
import Detail from "./Detail";

export default class Message extends Component {
    state = {
        messageArr: [
            { id: "01", title: "消息1" },
            { id: "02", title: "消息2" },
            { id: "03", title: "消息3" },
        ],
    };
    render() {
        const { messageArr } = this.state;
        return (
            <div>
                <ul>
                    {messageArr.map((msgObj) => {
                        return (
                            <li key={msgObj.id}>
                                {/* 向路由组件传递params参数 */}
                                {/* <Link to={`/home/message/detail/${msgObj.id}/${msgObj.title}`}>{msgObj.title}</Link> */}

                                {/* 向路由组件传递search参数 */}
                                {/* <Link to={`/home/message/detail/?id=${msgObj.id}&title=${msgObj.title}`}>{msgObj.title}</Link> */}

                                {/* 向路由组件传递state参数 */}
                                <Link
                                    to={{
                                        pathname: "/home/message/detail",
                                        state: {
                                            id: msgObj.id,
                                            title: msgObj.title,
                                        },
                                    }}
                                >
                                    {msgObj.title}
                                </Link>
                            </li>
                        );
                    })}
                </ul>
                <hr />
                {/* 声明接收params参数 */}
                {/* <Route path="/home/message/detail/:id/:title" component={Detail}/> */}

                {/* search参数无需声明接收，正常注册路由即可 */}
                {/* <Route path="/home/message/detail" component={Detail}/> */}

                {/* state参数无需声明接收，正常注册路由即可 */}
                <Route path="/home/message/detail" component={Detail} />
            </div>
        );
    }
}
```

#### 接收

```jsx
import React, { Component } from "react";
// import qs from 'querystring'

const DetailData = [
    { id: "01", content: "你好，中国" },
    { id: "02", content: "你好，尚硅谷" },
    { id: "03", content: "你好，未来的自己" },
];
export default class Detail extends Component {
    render() {
        console.log(this.props);

        // 接收params参数
        // const {id,title} = this.props.match.params

        // 接收search参数
        // const {search} = this.props.location
        // const {id,title} = qs.parse(search.slice(1))

        // 接收state参数
        const { id, title } = this.props.location.state || {};
        return (
            <ul>
                <li>ID:{id}</li>
                <li>TITLE:{title}</li>
                <li>CONTENT:{findResult.content}</li>
            </ul>
        );
    }
}
```

## 编程式导航

```jsx
import React, { Component } from "react";
import { Link, Route } from "react-router-dom";
import Detail from "./Detail";

export default class Message extends Component {
    state = {
        messageArr: [
            { id: "01", title: "消息1" },
            { id: "02", title: "消息2" },
            { id: "03", title: "消息3" },
        ],
    };

    replaceShow = (id, title) => {
        //replace跳转+携带params参数
        //this.props.history.replace(`/home/message/detail/${id}/${title}`)

        //replace跳转+携带search参数
        // this.props.history.replace(`/home/message/detail?id=${id}&title=${title}`)

        //replace跳转+携带state参数
        this.props.history.replace(`/home/message/detail`, { id, title });
    };

    pushShow = (id, title) => {
        //push跳转+携带params参数
        // this.props.history.push(`/home/message/detail/${id}/${title}`)

        //push跳转+携带search参数
        // this.props.history.push(`/home/message/detail?id=${id}&title=${title}`)

        //push跳转+携带state参数
        this.props.history.push(`/home/message/detail`, { id, title });
    };

    back = () => {
        this.props.history.goBack();
    };

    forward = () => {
        this.props.history.goForward();
    };

    go = () => {
        this.props.history.go(-2);
    };

    render() {
        const { messageArr } = this.state;
        return (
            <div>
                <ul>
                    {messageArr.map((msgObj) => {
                        return (
                            <li key={msgObj.id}>
                                {/* 向路由组件传递params参数 */}
                                {/* <Link to={`/home/message/detail/${msgObj.id}/${msgObj.title}`}>{msgObj.title}</Link> */}
                                {/* 向路由组件传递search参数 */}
                                {/* <Link to={`/home/message/detail/?id=${msgObj.id}&title=${msgObj.title}`}>{msgObj.title}</Link> */}
                                {/* 向路由组件传递state参数 */}
                                <Link
                                    to={{
                                        pathname: "/home/message/detail",
                                        state: {
                                            id: msgObj.id,
                                            title: msgObj.title,
                                        },
                                    }}
                                >
                                    {msgObj.title}
                                </Link>
                                &nbsp;
                                <button
                                    onClick={() =>
                                        this.pushShow(msgObj.id, msgObj.title)
                                    }
                                >
                                    push查看
                                </button>
                                &nbsp;
                                <button
                                    onClick={() =>
                                        this.replaceShow(
                                            msgObj.id,
                                            msgObj.title
                                        )
                                    }
                                >
                                    replace查看
                                </button>
                            </li>
                        );
                    })}
                </ul>
                <hr />
                {/* 声明接收params参数 */}
                {/* <Route path="/home/message/detail/:id/:title" component={Detail}/> */}
                {/* search参数无需声明接收，正常注册路由即可 */}
                {/* <Route path="/home/message/detail" component={Detail}/> */}
                {/* state参数无需声明接收，正常注册路由即可 */}
                <Route path="/home/message/detail" component={Detail} />
                <button onClick={this.back}>回退</button>&nbsp;
                <button onClick={this.forward}>前进</button>&nbsp;
                <button onClick={this.go}>go</button>
            </div>
        );
    }
}
```
