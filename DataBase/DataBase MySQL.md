## 启动/关停服务

### Windows 环境

```bash
NET START MySQL80
NET STOP MySQL80s
```

### Linux 环境

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

### 数据库的操作

#### 退出登录

```sql
exit;
```

#### 放弃指令

```sql
\c
```

#### 查看数据库

```sql
show databases;
```

## SQL 语句
