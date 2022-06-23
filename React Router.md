# React Router

## 使用

### 安装

```bash
npm i react-router-dom -s
```

### 引用

```javascript
import { HashRouter, Route, Link } from "react-router-dom";
```

> 这个包提供了三个核心的组件 **`HashRouter(BrowserRouter)`**, **`Route`**, **`Link`**

### 使用

使用 **`HashRouter`** 包裹整个应用，一个项目中只有一个 Router

使用 **`Link`** 指定导航链接

使用 **`Route`** 指定路由规则(哪个路径展示哪个组件)

使用 **`Switch`** 切换路由视图

```javascript
import React from "react";
import ReactDom from "react-dom";
import { HashRouter, Route, Link } from "react-router-dom";
import Search from "./pages/Search.jsx";
import Comment from "./pages/Comment.jsx";
export default function App() {
    return (
        <div>
            <h1>react路由基本使用</h1>
            <HashRouter>
                <Link to="/comment">评论</Link>
                <Link to="/search">搜索</Link>

                <Route path="/comment" component={Comment} />
                <Route path="/search" component={Search} />
            </HashRouter>
        </div>
    );
}
ReactDom.render(<App />, document.getElementById("root"));
```

## Router

### 两种模式

#### HashRouter

hash 模式

#### BrowserRouter

history 模式

### 内部原理

Router 组件：包裹整个应用，一个 React 应用只需要使用一次

两种常用 Router：`HashRouter` 和 `BrowserRouter`

-   HashRouter：使用 URL 的哈希值实现
    -   原理：监听 window 的 `hashchange` 事件来实现的
-   （推荐）BrowserRouter：使用 H5 的 history.pushState() API 实现
    -   原理：监听 window 的 `popstate` 事件来实现的

### 常规用法

使用 es6 的导入重命名来统一名字： 无论导入的是哪个路由对象，都叫 Router

```javascript
import { BrowserRouter as Router, Route, Link } from "react-router-dom";
import { HashRouter as Router, Route, Link } from "react-router-dom";
```

## Route

### 格式

#### 作用

决定路由匹配规则

#### 格式

```jsx
<Route path="/xx/xx" component={组件}></Route>
```

### 匹配规则

#### 属性解释

##### path

Route 组件中 path 属性的值

##### pathname

指的如下格式

##### link

组件中 to 的属性值，地址栏中的地址

#### 模糊匹配

> 默认模糊匹配

只要 pathname 以 path 开头就算匹配成功
匹配成功就加载对应组件；
整个匹配过程是逐一匹配，一个匹配成功了，并**不会停止匹配**。

精确匹配
补充**exact**可以设置成精确匹配

```jsx
import React from "react";
import ReactDom from "react-dom";
import { BrowserRouter as Router, Route, NavLink } from "react-router-dom";
const Home = () => <div>主页</div>;
const Article = () => <div>文章列表页</div>;
const ArticleDetail = () => <div>文章详情页</div>;
export default function App() {
    return (
        <div>
            <h1>react路由基本使用</h1>
            <Router>
                // 导航
                <NavLink to="/">主页</NavLink>&nbsp;
                <NavLink to="/article">文章列表页</NavLink>&nbsp;
                <NavLink to="/article/123">文章详情页-123</NavLink>&nbsp;
                <hr />
                // 对应的跳转规则
                <Route path="/" component={Home} />
                <Route path="/article" component={Article} />
                <Route path="/article/123" component={ArticleDetail} />
            </Router>
        </div>
    );
}
ReactDom.render(<App />, document.getElementById("root"));
```

### exact

如下代码:
如果不加`exact`精确匹配,name 所有以'/'开头的都会被这个 path 匹配到 ,如:'/home' , '/login'
加上`exact`精确匹配,只有在 path 为'/'的时候才能匹配到

```jsx
<Route path="/" exact component={Home} />
```

## Redirect

如下代码:

匹配到`from = '/'`后 , 重定向到 `"/comment"`路径对应的组件
这里的`from`页可以改写成`path`效果一样

```jsx
import { HashRouter, Route, Link, Redirect } from "react-router-dom";

<Redirect from="/" exact to="/comment" />;
```

## Link

无法指定当前高亮的路由

## NavLink

可以指定当前高亮的路由

## Switch

### 用法:

用 Switch 组件包裹多个`Route`组件。

在`Switch`组件下，不管有多少个 Route 的路由规则匹配成功，都只会渲染**第一个**匹配的组件

```jsx
import React from "react";
import ReactDom from "react-dom";
import {
    BrowserRouter as Router,
    Route,
    NavLink,
    Switch,
} from "react-router-dom";
const Home = () => <div>主页</div>;
const Article = () => <div>文章列表页</div>;
const ArticleDetail = () => <div>文章详情页</div>;
export default function App() {
    return (
        <div>
            <h1>react路由基本使用</h1>
            <Router>
                <NavLink to="/">主页</NavLink>&nbsp;
                <NavLink to="/article">文章列表页</NavLink>&nbsp;
                <NavLink to="/article/123">文章详情页-123</NavLink>&nbsp;
                <hr />
                <Switch>
                    <Route path="/" exact component={Home} />
                    <Route path="/article" component={Article} />
                    <Route path="/article/123" component={ArticleDetail} />
                </Switch>
            </Router>
        </div>
    );
}
ReactDom.render(<App />, document.getElementById("root"));
```

### 404 页面处理

通过`Switch`组件非常容易的就能实现 404 错误页面的提示

不设置 path 属性，将 404 页对应的路由放在 switch 内部的最后位置

```jsx
<Switch>
    <Route path="/" exact component={Home} />
    <Route path="/article" component={Article} />
    <Route path="/article/123" component={ArticleDetail} />
    <Route component={Page404} />
</Switch>
```

## 声明式导航

路由对象 Link 和 NavLink

Link 和 NavLink 都能用来做跳转,最终都会被渲染成`<a>内容</a>`标签
`import { Link, NavLink } from 'react-router-dom'`

### Link

`Link`组件无法展示哪个 link 处于选中的效果

```jsx
<Link to="/search">搜索</Link>
```

### NavLink

`NavLink`组件，一个更特殊的`Link`组件，可以用于指定当前导航高亮

格式：

```jsx
<NavLink to="/xxx" activeClassName="active">
    链接
</NavLink>
```

说明：

-   to 属性，用于指定地址，会渲染成 a 标签的 href 属性
-   activeClassName: 用于指定高亮的类名，默认`active`。一般不去修改

```jsx
return (
    <div>
        <h1>react路由基本使用-Link</h1>
        <Router>
            <div>
                Link:
                <Link to="/search">搜索</Link>
                <Link to="/comment">评论</Link>
            </div>
            <div>
                NavLink: 自带高亮类
                <NavLink to="/" exact>
                    主页
                </NavLink>
                <NavLink to="/search">搜索</NavLink>
                <NavLink to="/comment">评论</NavLink>
            </div>
            <Route path="/comment" component={Comment} />
            <Route path="/search" component={Search} />
        </Router>
    </div>
);
```

## 编程式导航

react-router

### history 对象

使用格式:

```jsx
import { useHistory } from "react-router-dom";

export default function App() {
    const history = useHistory();
    // 跳转到指定页面
    history.push("/home");

    // 前进或后退到某个页面，参数 n 表示前进或后退页面数量（比如：-1 表示后退到上一页）
    history.go(-1);

    // 替换到当前页面,展示指定页面
    history.replace("/login");
}
```

### history.replace 和 push 的区别

push：向历史记录中添加一条

replace：在历史记录中用目标记录来替换当前记录

**示例**

push:

```jsx
详情页  --> login页(push)  ----> 主页
```

此时，从主页后退，会回到 login 页。

replace

```jsx
详情页  --> login页(replace)  ----> 主页
```

此时，从主页后退，会回到详情页。

## 路由跳转传参

### location 对象

个人比较喜欢用`location`对象和 state,search 方式获取路由传值的操作,来看下 location 中有什么:

![Snipaste_2021-11-19_20-37-2png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/90d9d9c27dd04bef826e0f5ead4c6f99~tplv-k3u1fbpfcp-watermark.awebp?) **如何在组件中获取`location`对象:**

#### 组件中的 props 对象包含了 location:

```jsx
export default function Article(props) {
    console.log("props对象", props);
    return <div>Article</div>;
}
```

打印结果如图: ![location.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f41e51a27ad34d21b658266dd58be2b5~tplv-k3u1fbpfcp-watermark.awebp?)

#### history 中也包含了 location 对象

```jsx
import { useHistory } from "react-router-dom";
export default function Article() {
    const history = useHistory();
    console.log(history);
    return <div>Article</div>;
}
```

打印结果如图:

![history中的location.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/61045897e2da453dadadf7b2227d53eb~tplv-k3u1fbpfcp-watermark.awebp?)

#### useLocation 这个 Hook 获取

```jsx
import { useLocation } from "react-router-dom";
export default function Article() {
    const location = useLocation();
    console.log("使用useLocation获取的location", location);
    return <div>Article</div>;
}
```

打印结果如图: ![使用use hisahf .png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5114190e730b4729ba5fa16c79d84d3e~tplv-k3u1fbpfcp-watermark.awebp?)

### 声明式导航的传参:

#### 查询参数方式:

```jsx
<Link to="/home/article ?id=9 ">内容管理</Link>
```

#### 对象写法:

```jsx
// 传递单个id  (location.id拿值)
<Link to={{ pathname: '/home/article', id: 3 }}>内容管理</Link>

// 传递id 和 name (location.state拿值)
//这里写的如果不是state:{要传递的参数} ,那么location中原有的state属性会被覆盖,还是使用原有的state吧
<Link to={{ pathname: '/home/article', state: {id:3 , name:'给我一个div'} }}>内容管理</Link>
```

#### 接收数据:

再来看看传参之后`location`中有什么:
**查询参数方式**:

![查询参数.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9df4c5ed7d2f462d80e05f7b29f14f9f~tplv-k3u1fbpfcp-watermark.awebp?) **对象写法**

![state接收.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a607d7e1d14f4edea50006b87104ee4e~tplv-k3u1fbpfcp-watermark.awebp?)

#### 取值:

```
const value = location.state
const value = location.search
```

### 编程式导航的传参

同样的用`location`,`search`,`state`

```jsx
message.success("登录成功", 2, () => {
    //  做跳转动作 到主页中
    history.replace("/home?id=33");
});
```

`const value = location.search` //结果: ?id=33 需要截取一下

```jsx
message.success("登录成功", 2, () => {
    //  做跳转动作 到主页中
    history.replace("/home", "给我一个div");
});
```

`const value = location.state` //结果: 给我一个 div

```jsx
message.success("登录成功", 2, () => {
    //  做跳转动作 到主页中
    history.replace("/home", { name: "给我一个div", id: 9 });
});
```

`const value = location.state` // {name: '给我一个 div', id: 9}

### 路由传值小结:

个人比较喜欢这种方式传参,跳转的时候直接给参数,全部在 location 中接收参数,并且拿到 location 的方式也很方便
另外还有 params 方式传参,props 对象的 match 对象中有 params 对象,函数组件的话也可以使用`useParams`钩子 ,这里就不介绍了,想补充的兄弟欢迎在下面留言,有不对的地方欢迎指出
