# Linux 命令

## Linux 服务器操作

##### 删除文件夹、文件

```powershell
rm -f	#强制删除
rm -r	#删除子文件夹
sudo rm -rf  #文件夹的名字 sudo：授权操作的许可,提升权限
```

##### 查看 linux 内核版本

```
uname -r
```

##### 服务器密钥关联

```powershell
ssh-keygen -R 服务器端的 ip 地址
```

##### SSH 登录服务器

```powershell
ssh root@47.104.84.46 #远程登陆
```

##### 注销

```bash
 logout
```

##### 查看 IP、端口号

```bash
 netstat -ltnp // （Linux 服务器）
```

##### 查看系统信息

```
uname -a
```

## 服务部署操作

##### 启动某个服务

```bash
systemctl start docker
```

##### 重启某个服务

```bash
systemctl restart docker
```

##### FTP 文件上传

###### 对拷文件夹 (包括文件夹本身)

```bash
scp -r   /home/wwwroot/www/charts/util root@192.168.1.65:/home/wwwroot/limesurvey_back/scp
```

###### 对拷文件夹下所有文件 (不包括文件夹本身)

```bash
scp   /home/wwwroot/www/charts/util/* root@192.168.1.65:/home/wwwroot/limesurvey_back/scp
```

###### 对拷文件并重命名

```bash
scp   /home/wwwroot/www/charts/util/a.txt root@192.168.1.65:/home/wwwroot/limesurvey_back/scp/b.text
```
