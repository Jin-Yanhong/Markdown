# Linux 服务器

## Linux 服务器操作

### 删除文件夹、文件

```bash
rm -f	#强制删除
rm -r	#删除子文件夹
sudo rm -rf  #文件夹的名字 sudo：授权操作的许可,提升权限
```

### 查看文本文件内容

```bash
cat filename
```

### 查看 linux 内核版本

```
uname -r
```

### 服务器密钥关联

```bash
ssh-keygen -R 服务器端的 ip 地址
```

### SSH 登录服务器

```bash
ssh root@47.104.84.46 #远程登陆
```

### 注销

```bash
logout
```

### 查看 IP、端口号

```bash
netstat -ltnp # Linux 服务器
```

### 查看系统信息

```bash
uname -a
```

### 防火墙开放某个端口

```bash
firewall-cmd --add-port=80/tcp # 即时打开，这里也可以是一个端口范围，如1000-2000/tcp
```

### 关闭防火墙

```bash
systemctl stop firewalld.service
```

### 刷新系统服务

```bash
systemctl daemon-reload
```

##### 清空 DNS 缓存

```
systemctl restart dnsmasq.service
```

## 服务部署操作

### 启动某个服务

```bash
systemctl start docker
```

### 重启某个服务

```bash
systemctl restart docker
```

#### 修改 Hosts 文件

```
vim /etc/hosts
```

## 服务器磁盘操作

### Linux rm

（英文全拼：remove）命令用于删除一个文件或者目录。

#### 语法

```
rm [options] name...
```

**参数：**

-   -i 删除前逐一询问确认。
-   -f 即使原档案属性设为唯读，亦直接删除，无需逐一确认。
-   -r 将目录及以下之档案亦逐一删除。

#### 实例

```bash
rm  -rf  homework
# rm：是否删除 目录 "homework"? y
```

> **`rm -rf`** 强制删除，不做任何提示

### Linux mv

英文全拼：move file 命令用来为文件或目录改名、或将文件或目录移入其它位置。

#### 语法

```
mv [options] source dest
mv [options] source... directory
```

**参数说明**：

-   **-b**: 当目标文件或目录存在时，在执行覆盖前，会为其创建一个备份。
-   **-i**: 如果指定移动的源目录或文件与目标的目录或文件同名，则会先询问是否覆盖旧文件，输入 y 表示直接覆盖，输入 n 表示取消该操作。
-   **-f**: 如果指定移动的源目录或文件与目标的目录或文件同名，不会询问，直接覆盖旧文件。
-   **-n**: 不要覆盖任何已存在的文件或目录。
-   **-u**：当源文件比目标文件新或者目标文件不存在时，才执行移动操作。

#### 实例

-   将文件 aaa 改名为 bbb :

```bash
mv aaa bbb
```

-   将 info 目录放入 logs 目录中。注意，如果 logs 目录不存在，则该命令将 info 改名为 logs。

```bash
mv info/ logs
```

-   再如将 **/usr/runoob** 下的所有文件和目录移到当前目录下，命令行为：

```bash
$ mv /usr/runoob/*  .
```

-   把当前目录下的所有文件 移动到 **`/home/app/web`** 这个文件夹

```bash
 mv ./*  /home/app/web
```

### Linux scp

命令用于 Linux 之间复制文件和目录。

scp 是 secure copy 的缩写, scp 是 linux 系统下基于 ssh 登陆进行安全的远程文件拷贝命令。

scp 是加密的，[rcp](https://www.runoob.com/linux/linux-comm-rcp.html) 是不加密的，scp 是 rcp 的加强版。

#### 语法

```bash
scp [-1246BCpqrv] [-c cipher] [-F ssh_config] [-i identity_file]
[-l limit] [-o ssh_option] [-P port] [-S program]
[[user@]host1:]file1 [...] [[user@]host2:]file2
```

**参数说明：**

-   -1： 强制 scp 命令使用协议 ssh1
-   -2： 强制 scp 命令使用协议 ssh2
-   -4： 强制 scp 命令只使用 IPv4 寻址
-   -6： 强制 scp 命令只使用 IPv6 寻址
-   -B： 使用批处理模式（传输过程中不询问传输口令或短语）
-   -C： 允许压缩。（将-C 标志传递给 ssh，从而打开压缩功能）
-   -p：保留原文件的修改时间，访问时间和访问权限。
-   -q： 不显示传输进度条。
-   -r： 递归复制整个目录。
-   -v：详细方式显示输出。scp 和 ssh(1)会显示出整个过程的调试信息。这些信息用于调试连接，验证和配置问题。
-   -c cipher： 以 cipher 将数据传输进行加密，这个选项将直接传递给 ssh。
-   -F ssh_config： 指定一个替代的 ssh 配置文件，此参数直接传递给 ssh。
-   -i identity_file： 从指定文件中读取传输时使用的密钥文件，此参数直接传递给 ssh。
-   -l limit： 限定用户所能使用的带宽，以 Kbit/s 为单位。
-   -o ssh_option： 如果习惯于使用 ssh_config(5)中的参数传递方式，
-   -P port：注意是大写的 P, port 是指定数据传输用到的端口号
-   -S program： 指定加密传输时所使用的程序。此程序必须能够理解 ssh(1)的选项。

#### 实例

**文件夹包括文件夹本身**

```bash
scp -r   /home/wwwroot/www/charts/util root@192.168.1.65:/home/wwwroot/limesurvey_back/scp
```

**文件夹下所有文件不包括文件夹本身**

```bash
scp   /home/wwwroot/www/charts/util/* root@192.168.1.65:/home/wwwroot/limesurvey_back/scp
```

**文件并重命名**

```bash
scp   /home/wwwroot/www/charts/util/a.txt root@192.168.1.65:/home/wwwroot/limesurvey_back/scp/b.text
```

### Linux whereis

命令用于查找文件。

该指令会在特定目录中查找符合条件的文件。这些文件应属于原始代码、二进制文件，或是帮助文件。

该指令只能用于查找二进制文件、源代码文件和 man 手册页，一般文件的定位需使用 locate 命令。

#### 语法

```bash
whereis [-bfmsu][-B <目录>...][-M <目录>...][-S <目录>...][文件...]
```

**参数：**

-   -b 　只查找二进制文件。

-   -B<目录> 　只在设置的目录下查找二进制文件。

-   -f 　不显示文件名前的路径名称。

-   -m 　只查找说明文件。

-   -M<目录> 　只在设置的目录下查找说明文件。

-   -s 　只查找原始代码文件。

-   -S<目录> 　只在设置的目录下查找原始代码文件。

-   -u 　查找不包含指定类型的文件。

#### 实例

使用指令"whereis"查看指令"bash"的位置，输入如下命令：

```bash
$ whereis bash
```

上面的指令执行后，输出信息如下所示：

```bash
bash:/bin/bash/etc/bash.bashrc/usr/share/man/man1/bash.1.gz
```

注意：以上输出信息从左至右分别为查询的程序名、bash 路径、bash 的 man 手册页路径。

如果用户需要单独查询二进制文件或帮助文件，可使用如下命令：

```bash
$ whereis -b bash
$ whereis -m bash
```

输出信息如下：

```bash
$ whereis -b bash               #显示bash 命令的二进制程序
bash: /bin/bash /etc/bash.bashrc /usr/share/bash    # bash命令的二进制程序的地址
$ whereis -m bash               #显示bash 命令的帮助文件
bash: /usr/share/man/man1/bash.1.gz  #bash命令的帮助文件地址
```

## Web 服务器应用

### 单页面应用刷新 **`404`** 问题

#### Nginx

```ini
location / {
  try_files $uri $uri/ /index.html;
}
```

#### Apache

```xml
<IfModule mod_rewrite.c>
  RewriteEngine On
  RewriteBase /
  RewriteRule ^index\.html$ - [L]
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule . /index.html [L]
</IfModule>
```

## 项目信息查看

### 根据端口号查找项目路径

1.  使用 netstat 来查看端口对应的的 pid

```bash
netstat -antlp | grep 9002 #端口号
netstat -tunlp | grep 9002 #端口号
```

2.  使用 cd 打开 pid 所在的文件路径

```bash
cd  /proc/{上一步查询出的pid号}
```

3.  获取该进程所在目录

```bash
pwdx {上一步查询出的pid号}
```

4.  查看进程占用哪些文件的

```bash
lsof -i:8080
```

5.  查看某个文件被哪个进程占用的

```bash
fuser -m -v /data/
```

### 配置服务自启动

```bash

```
