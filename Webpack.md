## npm 命令行参数

```bash
// 安装开发所用的依赖
npm i -D
npm i -Dev
npm install -D webpack-cli
npm install -g webpack-dev-server
npm install -D webpack
npm install -D @babel/core @babel/preset-env babel-loader core.js
```

-   配置文件 webpack.config.js

```javascript
// 引入一个包，用于拼接路径
const path = require("path");
// 引入html插件
const HtmlWebpackplugin = require("html-webpack-plugin");
const { CleanWebpackPlugin } = require("clean-webpack-plugin");
// 包含webpack所有的配置信息
module.exports = {
    // 指定入口文件
    entry: "./demo.js",
    // 指定打包文件所在目录
    output: {
        // 指定打包文件的目录
        path: path.resolve(__dirname, "dist"),
        // 打包文件
        filename: "bundle.js",
        // 配置打包后的环境
        environment: {
            // 不使用箭头函数
            arrowFunction: false,
        },
    },
    // 指定webpack打包时要加载的模块
    module: {
        // 指定加载规则
        rules: [
            {
                // 指定规则生效的文件
                test: /.ts$/,
                // 要使用的loader,loader 的使用顺序是后来居上的，配置在后边的loader先使用，
                use: [
                    {
                        loader: "babel-loader",
                        options: {
                            //设置预先定义的运行环境
                            presets: [
                                [
                                    "@babel/preset-env",
                                    {
                                        // 运行环境 要兼容的浏览器
                                        targets: {
                                            chrome: 88,
                                            ie: "11",
                                        },
                                        corejs: "3",
                                        // s使用corejs的方式
                                        useBuiltIns: "usage", // 按需加载
                                    },
                                ],
                            ],
                        },
                    },
                    "ts-loader",
                ],
                // 要排除deloader
                exclude: /node_modules/,
            },
        ],
    },
    plugins: [
        new CleanWebpackPlugin(),
        new HtmlWebpackplugin({
            // 指定网页标题
            title: "your title",
            // 指定网页模板文件的路径
            template: "./src/template.html",
        }),
    ],
    // 用来设置引用模块
    resolve: {
        extensions: [".js", "ts"],
    },
};
```

-   配置 package.json

```json
{
    "name": "demo",
    "version": "1.0.0",
    "description": "",
    "main": "Demo.js",
    "dependencies": {
        "html-webpack-plugin": "^5.2.0",
        "webpack": "^5.24.2"
    },
    "devDependencies": {
        "webpack-cli": "^4.5.0",
        "webpack-dev-server": "^3.11.2"
    },
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1",
        "build": "webpack",
        "start": "webpack serve --open chrome.exe"
    },
    "author": "",
    "license": "ISC"
}
```

## 编译原理
