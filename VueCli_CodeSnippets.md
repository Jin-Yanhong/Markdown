## Route

-   传递参数
    ```javascript
    this.$router.push({
        name: '', //此处的 name 是路由 路径下的 name 属性
        params: {
            page: '1',
            code: '8989',
        },
    });
    ```
-   接收参数
-   ```javascript
    this.page = this.$route.params.page; // 用$route接收，少个r,注意
    ```
-   npm i --save animate.css@3
    
-   函数方法的执行要略微晚于 DOM 的加载，写在 DOM 里的方法可以用箭头函数执行

## Watch

监听路由

-   方法一

```javascript
// 
watch:{
  $route(to,from){
    console.log(to.path);
  }
}, 
```

-   方法二

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

-   方法三

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

