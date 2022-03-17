# MySQL 命令

## 启动/关停服务

### Windows 下

```bash
NET START MySQL80
NET STOP MySQL80s
```

### Linux 下

```bash
systemctl start mysqld
systemctl stop mysqld
systemctl status mysqld
```

## MySQL 的基本操作

#### 链接 数据库

```bash
mysql -uroot -p;（也可以把密码直接跟在后边）
mysql -uroot -p -P3306 -h 127.0.0.1;（端口号+主机地址）
```

#### 退出登录

```mysql
exit;
```

#### 查看数据库

```mysql
show databases; # 分号不能丢
```

#### 放弃指令（比如指令错误）

```mysql
\c
```

## 数据库的基本操作

#### 创建数据库

```mysql
# 创建数据库shop，并指定字符集
create database shop charset utf8;
```

#### 使用数据库

```mysql
use shop
```

#### 查看当前数据库

```mysql
// 查看当前数据库
show databases shop
```

#### 修改数据表名称（重命名）

```mysql
ALTER TABLE oldName RENAME newName;
RENAME TABLE stus to stu
```

#### 删除数据库

```mysql
drop  database if exists tableName;
```

#### 导入外部（.sql）文件

```mysql
mysql -uroot -p < .sql文件
source .sql文件
```

## 数据表的操作 table

-   新增数据表

```mysql
create table tableName (id INT );
CREATE table stu (id INT PRIMARY KEY AUTO_INCREMENT, sname CHAR ( 10 ), class_id INT DEFAULT NULL,age SMALLINT NOT NULL);
-- 从已有数据表复制新的数据表 --
create table tableName select * from existTable
```

-   删除数据表

```mysql
drop tabel if exists tableName;
TRUNCATE tableName

```

## 数据字段的操作

#### 降序/升序排列

```mysql
-- 降序
desc;
-- 升序
acs;
```

#### 插入数据

```mysql
insert info tableName set key = “val”,key=“val”;
insert info tableName (key1,key2) values (“val1”,“val2”);
```

#### 修改字段

```mysql
-- 修改数据格式
ALTER table tableName MODIFY fieldName varchar(20) not null;

-- 修改字段名称
ALTER table tableName CHANGE fieldName existFieldName newFieldName not null;

-- 在指定位置插入新的字段（after）
ALTER table tableName ADD newFieldName smallint default null AFTER fieldName1
-- 添加一个字段作为首个字段 （first）
ALTER table tableName ADD newFieldName smallint default null first

-- 删除某个字段
ALTER table tableName drop field
```

## 数据的基本操作

### 数据的查询

#### 全部查询

-   ```mysql
    SELECT * FROM tableName
    ```
-   ```mysql
    desc tableName
    ```
-   ```mysql
    SELECT name ,id as ids FROM tableName // as 表示别名
    ```

##### 条件查询

###### **查询所有**

-   ```mysql
    select * from class WHERE id > 2 // 查找所有id > 2 的数据
    ```
-   ```sql
    // 查找所有 cname = 'php' 的数据
    select * from class WHERE cname = 'php'
    ```
-   ```sql
    // 查询条件不包含
      select * from class WHERE description not like'%p%' and id > 2// 查找所有描述字段不包含p,并且id > 2 的数据
    ```
-   ```mysql
    // 查找所有描述字段不包含p的数据,或者id > 2 的数据
    select * from class WHERE description not like'%p%' or id > 2
    ```
-   ```sql
    // 查找所有年龄介于20 ~ 30 之间的
    select * from class WHERE age BETWEEN 20 and 30
    ```
-   ```mysql
    // 查找所有班级id介于2 ~ 3 之间的
    select * from class WHERE class_id in(2,3)
    ```
-   ```sql
    // 查找所有班级id不在2 ~ 3 之间的
    select * from class WHERE class_id in(2,3)
    ```
-   ```mysql
    //对null的操作
      select * from class WHERE class_id is null
    ```

###### 查询部分字段

-   ```sql
    select name,id from class where
    ```
-   ```sql
    // 字段别名
    select name,id as ids from class
    ```
-   ```sql
    // 使用连接函数
    select CONCAT(cname,description) as class_info from class
    返回的结果会以 class_info 为新的字段名
    ```

-   数据的新增

    ```mysql

    ```

## 数据字段类型

## 排序规则

-   **ci** 对大小写不敏感（Case insensitive）
