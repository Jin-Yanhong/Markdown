## 系统服务

### Cent OS 卸载

1. 停止服务

```bash
sudo service mongod stop
```

2. 查看 mongo 相关的包

```bash
yum list installed | grep mongo
```

3. 移除相关的包

```bash
sudo yum erase $(rpm -qa | grep mongodb-org)
```

4. 删除日志、数据文件

```bash
sudo rm -r /var/log/mongodb
sudo rm -r /var/lib/mongo
```

### Cent OS 安装

[官方文档](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-enterprise-on-red-hat/)

## 数据库配置

### 首次安装添加管理员用户

```javascript
use admin

db.createUser({
    user: "root", // 用户名
    pwd: "root", // 密码
    roles: [
        {
            role: "root", // 角色
            db: "admin", // 数据库
        },
    ],
});
```

### 指定数据库路径

```bash
mongod --dbpath D:\DevTools\MongoDB\data --port 27017
```

## 基本指令

### 显示所有数据库

```javascript
show dbs / show databases
```

### 指定数据库

```javascript
use db_name
```

### 当前数据库

```javascript
db;
```

### 显示当前数据库所有集合

```javascript
show collections
```

## CRUD 指令

### 插入文档

```javascript
db.collection.insert();
```

```javascript
db.collection.insertOne();
```

```javascript
db.collection.insertMany();
```

> id 属性数据库系统会默认生成，也可以自己指定 id，并确保 id 的唯一性

### 查询文档

```javascript
db.collection.find({}, {});
// 该方法返回数组，第二个参数配置查询需要返回的字段 {key:1,id:0 }
```

```javascript
// 查询长度;
db.collection.find().count();

db.collection.find().length();
```

```javascript
db.collection.findOne();
// 返回对象;
```

### 修改文档

```javascript
db.collection.update(filter, update, options);
```

> 默认情况 只修改一个

```javascript
db.collection.updateOne(filter, update, options);
```

```javascript
db.collection.updateMany(filter, update, options);
```

```javascript
db.collection.replaceOne(filter, update, options);
```

update 会用新对象替换查找到的对象，如果西药修改指定的属性，需要使用 修改操作符 来完成，常用的 修改操作符 [点击这里](https://www.mongodb.com/docs/v4.2/reference/operator/update/)

### 删除文档

```javascript
// 删除满足条件的所有文档（多个）
db.collection.remove();
```

```javascript
db.collection.deleteOne();
```

```javascript
db.collection.deleteMany();
```

### 删除集合

```javascript
db.collection.drop();
```

### 删除数据库

```javascript
// 实际生产过程中，都是软删除
db.dropDatabase();
```

### 文档排序

默认按照创建时间升序排序

```javascript
db.collection.find().sort({
    key: 1,
});

// 1 升序
// -1 降序
```

```javascript
db.collection.find().limit();
```

```javascript
db.collection.find().skip();
```

## Mongoose

### 核心对象

#### Schema

[参考文档](https://mongoosejs.com/docs/api/schema.html)

#### Model

[参考文档](https://mongoosejs.com/docs/api/model.html)

#### Document

[参考文档](https://mongoosejs.com/docs/api/document.html)

### 安装

```bash
npm i mongoose --save
```

### 应用

#### 连接数据库

```javascript
const mongoose = require("mongoose");

mongoose.connect("mongodb://localhost/my_database", {
    useMongoClient: true,
});

mongoose.connection.once("open", function () {});

mongoose.connection.once("close", function () {});

const blogSchema = new mongoose.Schema({
    title: String, // String is shorthand for {type: String}
    author: String,
    body: String,
    comments: [{ body: String, date: Date }],
    date: { type: Date, default: Date.now },
    hidden: Boolean,
    meta: {
        votes: Number,
        favs: Number,
    },
});

const BlogModel = mongoose.model("Blog", blogSchema);
```

#### CRUD

点击[这里](https://mongoosejs.com/docs/api/model.html)查看文档

```

```
