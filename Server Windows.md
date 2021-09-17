## 端口相关

##### 查看端口占用情况

```bash
netstat -ano
```

##### 查看被占用端口对应的 PID

```bash
netstat -aon|findstr "8081"
```

##### 查看指定 PID 的进程

```bash
tasklist|findstr "9088"
```

## 启动相关服务

##### 启动

```bash
NET START 服务名
```

##### 停止

```bash
NET STOP 服务名
```
