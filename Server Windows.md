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

## 系统相关服务

##### 启动

```bash
NET START 服务名
```

##### 停止

```bash
NET STOP 服务名
```

##### 安装相关服务

```bash
service install serviceName
```

##### 清空 DNS 缓存

```
systemctl restart dnsmasq.service
```

##### Windows 刷新环境变量

```bash
set PATH=C
exit;
echo %PATH%
```

## 文件操作

##### 查看文本文件内容

```bash
cat filename
```

##### 拷贝文本文件的内容

```sh
clip < filepath filename
```

```sh
# 环境变量
set PATH=C
echo %PATH%
```
