# Vue Route

## 参数传递与接收

### 方法一

```javascript
this.$router.push({
    path: `/particulars/${id}`,
});
```

```javascript
// 对应的路由需要如下配置
{
    path: "/particulars/:id";
}
```

```javascript
// 用$route接收，少个r,注意
this.$route.params.id;
```

### 方法二

```javascript
this.$router.push({
    name: "particulars",
    params: {
        id: id,
    },
});
```

```javascript
// 注意这里不能使用:/id来传递参数了，因为组件中，已经使用params来携带参数了
{
    path: "/particulars";
}
```

```javascript
this.$route.params.id;
```

### 方法三

```javascript
this.$router.push({
    path: "/particulars",
    query: {
        id: id,
    },
});
```

```javascript
{
    path: "/particulars";
}
```

```javascript
this.$route.query.id;
```

## 路由监听

### 方法一

```javascript
watch:{
    $route(to,from){
        console.log(to.path)
    }
},
```

### 方法二

```javascript
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

### 方法三

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

> 函数方法的执行要略微晚于 DOM 的加载，写在 DOM 里的方法可以用箭头函数执行
