# MongoDB 数据库

## 服务配置

### 首次安装添加管理员用户

```javascript
use admin
db.createUser({
  user: 'root',  // 用户名
  pwd: 'root',  // 密码
  roles:[{
    role: 'root',  // 角色
    db: 'admin'  // 数据库
  }]
})
```

### 指定数据库路径

```bash
mongod --dbpath D:\DevTools\MongoDB\data
```
