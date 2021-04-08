# VueX

---

### 核心概念

#### state

> key-value

```javascript
// user/store.js
state: {
    token: getToken(),
    name: "",
    avatar: "",
    roles: [],
    permissions: []
},
```

#### getters

> 可以认为是 store 的计算属性
>
> 接受 state 作为其第一个参数
>
> 会暴露为 `store.getters` 对象，你可以以属性的形式访问

```javascript
// user/store.js
getters: {
  // ...
  doneTodosCount: (state, getters) => {
    return getters.doneTodos.length
  }
}
// use.vue 计算属性
computed: {
  doneTodosCount () {
    return this.$store.getters.doneTodosCount
  }
}
```

#### mutations

> **必须同步执行**，不接受异步
>
> 直接触发状态的改变

```javascript
// user/store.js
mutations: {
      // 状态更改
    SET_TOKEN: (state, token) => {
      state.token = token;
    },
    SET_NAME: (state, name) => {
      state.name = name;
    },
    SET_AVATAR: (state, avatar) => {
      state.avatar = avatar;
    },
    SET_ROLES: (state, roles) => {
      state.roles = roles;
    },
    SET_PERMISSIONS: (state, permissions) => {
      state.permissions = permissions;
    }
},
```

> 每个 mutation 都有一个字符串的 **事件类型 (type)** 和 一个 **回调函数 (handler)**
>
> 回调函数就是我们实际进行状态更改的地方，并且它会接受 state 作为第一个参数
>
> 可以向 `store.commit` 传入额外的参数，即 mutation 的 **载荷（payload）**

#### actions

> 通过 `store.commit` 提交 **mutations** 里的方法，触发状态变更，本质上是方法，还可以处理其他逻辑，
>
> 可以在`action`内执行异步方法

```javascript
// user/store.js
import { getInfo, login, logout } from "@/api/login";
import { getToken, removeToken, setToken } from "@/utils/auth";
actions: {
    // 提交 mutations ，触发状态变更
    // 登录
    Login({ commit }, userInfo) {
      const username = userInfo.username.trim();
      const password = userInfo.password;
      const code = userInfo.code;
      const uuid = userInfo.uuid;
      return new Promise((resolve, reject) => {
        login(username, password, code, uuid)
          .then(res => {
            setToken(res.token);
            commit("SET_TOKEN", res.token);
            resolve();
          })
          .catch(error => {
            reject(error);
          });
      });
    },
    // 获取用户信息
    GetInfo({ commit, state }) {
      return new Promise((resolve, reject) => {
        getInfo()
          .then(res => {
            const user = res.user;
            const avatar =
              user.avatar == ""
                ? require("@/assets/images/profile.jpg")
                : process.env.VUE_APP_BASE_API + user.avatar;
            if (res.roles && res.roles.length > 0) {
              // 验证返回的roles是否是一个非空数组
              commit("SET_ROLES", res.roles);
              commit("SET_PERMISSIONS", res.permissions);
            } else {
              commit("SET_ROLES", ["ROLE_DEFAULT"]);
            }
            commit("SET_NAME", user.userName);
            commit("SET_AVATAR", avatar);
            resolve(res);
          })
          .catch(error => {
            reject(error);
          });
      });
    },
    // 退出系统
    LogOut({ commit, state }) {
      return new Promise((resolve, reject) => {
        logout(state.token)
          .then(() => {
            commit("SET_TOKEN", "");
            commit("SET_ROLES", []);
            commit("SET_PERMISSIONS", []);
            removeToken();
            resolve();
          })
          .catch(error => {
            reject(error);
          });
      });
    },
    // 前端 登出
    FedLogOut({ commit }) {
      return new Promise(resolve => {
        commit("SET_TOKEN", "");
        removeToken();
        resolve();
      });
    }
  }
};
```

-   commit 也可以这么写

```javascript
// 以对象形式分发
store.commit({
    type: '',
    key: value,
});
// type:mutations里的方法名
// key:需要传递的参数
// value:参数的值
// 以载荷形式分发
store.commit({ type, key: value });
```

-   在组件中分发 action

```javascript
// login.vue
// 在方法中触发
this.$store.dispatch('Login', this.loginForm)
// 在 methods 中使用辅助函数
import { mapActions } from 'vuex'
...mapActions([
  'Login', // 将 `this.login(form)` 映射为 `this.$store.dispatch('Login',form)`
]),
...mapActions({
  add: 'increment' // 将 `this.add()` 映射为 `this.$store.dispatch('increment')`
})
```

> Action 函数接受一个与 store 实例具有相同方法和属性的 context 对象，因此你可以调用 `context.commit` 提交一个 mutation，或者通过 `context.state` 和 `context.getters` 来获取 state 和 getters。
>
> 在前面定义 actions 的时候返回 Promise，后续分发中可以使用
>
> ```js
> store.dispatch('actionA').then(() => {
>     // ...
> });
> ```
>
> 的处理方式

#### modules

> 模块化

```javascript
// user/store.js
export default user;
// store/index.js
import user from './modules/user';
const store = new Vuex.Store({
    modules: {
        user,
    },
});
export default store;
// main.js 入口文件
import store from './store';
new Vue({
    store,
});
```

-   模块的局部状态
    > 对于模块内部的 mutation 和 getter，接收的第一个参数是模块的局部状态对象。

```js
const moduleA = {
    state: () => ({
        count: 0,
    }),
    mutations: {
        increment(state) {
            // 这里的 `state` 对象是模块的局部状态
            state.count++;
        },
    },
    getters: {
        doubleCount(state) {
            return state.count * 2;
        },
    },
};
```

> 同样，对于模块内部的 action，局部状态通过 `context.state` 暴露出来，根节点状态则为 `context.rootState`

```js
const moduleA = {
    // ...
    actions: {
        incrementIfOddOnRootSum({ state, commit, rootState }) {
            if ((state.count + rootState.count) % 2 === 1) {
                commit('increment');
            }
        },
    },
};
```

对于模块内部的 getter，根节点状态会作为第三个参数暴露出来：

```javascript
const moduleA = {
    // ...
    getters: {
        sumWithRootCount(state, getters, rootState) {
            return state.count + rootState.count;
        },
    },
};
```

### 辅助函数

#### mapGetters

> 仅仅是将 store 中的 getter 映射到局部计算属性

```javascript
import { mapGetters } from 'vuex';
export default {
    // ...
    computed: {
        // 使用对象展开运算符将 getter 混入 computed 对象中
        ...mapGetters([
            'doneTodosCount',
            'anotherGetter',
            // ...
        ]),
    },
};
```

> 可以将一个 getter 属性另取一个名字，使用对象形式：

```javascript
...mapGetters({
  // 把 `this.doneCount` 映射为 `this.$store.getters.doneTodosCount`
  doneCount: 'doneTodosCount'
})
```
