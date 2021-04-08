## 端口相关

-   查看端口占用情况

```bash
netstat -ano
```

-   查看被占用端口对应的 PID

```bash
netstat -aon|findstr "8081"
```

-   查看指定 PID 的进程

```bash
tasklist|findstr "9088"
```
