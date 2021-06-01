全局安装 vue Cli

```bash
npm i -g vue-cli
npm i -g @vue/cli@4.5.8
// 更新 Vue 之前需要卸载旧版本
```

安装淘宝镜像

```bash
npm i -g cnpm --registry=https://registry.npm.taobao.org
```

指定淘宝镜像源

```bash
npm config set registry https://registry.npm.taobao.org
```

验证是否配置成功
常用组件

```bash
npm install --save axios vue-axios
npm i vant -S
npm install axios
npm i element-ui -S
```

创建 Vue-Cli 脚手架项目

```bash
vue init webpack my-project
vue create my-project
```

安装路由管理模块

```bash
npm install vue-router --save
```

安装状态管理模块

```bash
npm install vuex --save
```

安装 vueResource

```bash
npm install vue-resource
```

安装 EChart

```bash
npm install echarts --registry=https://r.npm.taobao.org echarts
```

安装 jsonp

```bash
cnpm install --save jsonp
```

安装 Swiper（版本兼容性问题）

```bash
npm install vue-awesome-swiper@3 --save-dev
```

\*.vue 引用

```javascript
import { swiper, swiperSlide } from 'vue-awesome-swiper';
import 'swiper/dist/css/swiper.css';
```

main.js 全局引用

```javascript
//swiper 轮播图插件
import 'swiper/dist/css/swiper.css';
import VueAwesomeSwiper from 'vue-awesome-swiper';
Vue.use(VueAwesomeSwiper);
```

开启热更新

```js
// vue.config.js
devServer: {
    compress: true,
    disableHostCheck: true, //webpack4.0 开启热更新
}
// package.json
"serve": "vue-cli-service serve && webpack-dev-server --open",
```
