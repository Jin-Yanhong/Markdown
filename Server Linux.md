# Linux 服务器

## 磁盘目录

![img](https://blog-pic-store.oss-cn-beijing.aliyuncs.com/blog/d0c50-linux2bfile2bsystem2bhierarchy.jpg)

### 目录解释

#### /bin

    bin 是 Binaries (二进制文件) 的缩写, 这个目录存放着最经常使用的命令。

#### /boot

    这里存放的是启动 Linux 时使用的一些核心文件，包括一些连接文件以及镜像文件。

#### /dev

    dev 是 Device(设备) 的缩写, 该目录下存放的是 Linux 的外部设备，在 Linux 中访问设备的方式和访问文件的方式是相同的。

#### /etc

    etc 是 Etcetera(等等) 的缩写,这个目录用来存放所有的系统管理所需要的配置文件和子目录。

#### /home

    用户的主目录，在 Linux 中，每个用户都有一个自己的目录，一般该目录名是以用户的账号命名的，如上图中的 alice、bob 和 eve。

#### /lib

    lib 是 Library(库) 的缩写这个目录里存放着系统最基本的动态连接共享库，其作用类似于 Windows 里的 DLL 文件。几乎所有的应用程序都需要用到这些共享库。

#### /lost+found

    这个目录一般情况下是空的，当系统非法关机后，这里就存放了一些文件。

#### /media

    linux 系统会自动识别一些设备，例如 U 盘、光驱等等，当识别后，Linux 会把识别的设备挂载到这个目录下。

#### /mnt

    系统提供该目录是为了让用户临时挂载别的文件系统的，我们可以将光驱挂载在 /mnt/ 上，然后进入该目录就可以查看光驱里的内容了。

#### /opt

    opt 是 optional(可选) 的缩写，这是给主机额外安装软件所摆放的目录。比如你安装一个 ORACLE 数据库则就可以放到这个目录下。默认是空的。

#### /proc

    proc 是 Processes(进程) 的缩写，/proc 是一种伪文件系统（也即虚拟文件系统），存储的是当前内核运行状态的一系列特殊文件，这个目录是一个虚拟的目录，它是系统内存的映射，我们可以通过直接访问这个目录来获取系统信息。
    这个目录的内容不在硬盘上而是在内存里，我们也可以直接修改里面的某些文件，比如可以通过下面的命令来屏蔽主机的 ping 命令，使别人无法 ping 你的机器：

    ```
    echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_all
    ```

#### /root

    该目录为系统管理员，也称作超级权限者的用户主目录。

#### /sbin

    s 就是 Super User 的意思，是 Superuser Binaries (超级用户的二进制文件) 的缩写，这里存放的是系统管理员使用的系统管理程序。

#### /selinux

    这个目录是 Redhat/CentOS 所特有的目录，Selinux 是一个安全机制，类似于 windows 的防火墙，但是这套机制比较复杂，这个目录就是存放 selinux 相关的文件的。

#### /srv

    该目录存放一些服务启动之后需要提取的数据。

#### /sys

    这是 Linux2.6 内核的一个很大的变化。该目录下安装了 2.6 内核中新出现的一个文件系统 sysfs 。

    sysfs 文件系统集成了下面 3 种文件系统的信息：针对进程信息的 proc 文件系统、针对设备的 devfs 文件系统以及针对伪终端的 devpts 文件系统。

    该文件系统是内核设备树的一个直观反映。

    当一个内核对象被创建的时候，对应的文件和目录也在内核对象子系统中被创建。

#### /tmp

    tmp 是 temporary(临时) 的缩写这个目录是用来存放一些临时文件的。

#### /usr

    usr 是 unix shared resources(共享资源) 的缩写，这是一个非常重要的目录，用户的很多应用程序和文件都放在这个目录下，类似于 windows 下的 program files 目录。

#### /usr/bin

    系统用户使用的应用程序。

#### /usr/sbin

    超级用户使用的比较高级的管理程序和系统守护程序。

#### /usr/src

    内核源代码默认的放置目录。

#### /var

    var 是 variable(变量) 的缩写，这个目录中存放着在不断扩充着的东西，我们习惯将那些经常被修改的目录放在这个目录下。包括各种日志文件。

#### /run

    是一个临时文件系统，存储系统启动以来的信息。当系统重启时，这个目录下的文件应该被删掉或清除。如果你的系统上有 /var/run 目录，应该让它指向 run。

在 Linux 系统中，有几个目录是比较重要的，平时需要注意不要误删除或者随意更改内部文件。

### 特别注意的目录

#### /etc

上边也提到了，这个是系统中的配置文件，如果你更改了该目录下的某个文件可能会导致系统不能启动。

#### /var

这是一个非常重要的目录，系统上跑了很多程序，那么每个程序都会有相应的日志产生，而这些日志就被记录到这个目录下，具体在 /var/log 目录下，另外 mail 的预设放置也是在这里。

#### /bin, /sbin, /usr/bin, /usr/sbin

这是系统预设的执行文件的放置目录，比如 ls 就是在 /bin/ls 目录下的。

值得提出的是，/bin, /usr/bin 是给系统用户使用的指令（除 root 外的通用户），而/sbin, /usr/sbin 则是给 root 使用的指令。

## Linux 服务器操作

### 删除文件夹、文件

```bash
rm -f	#强制删除
rm -r	#删除子文件夹
sudo rm -rf  #文件夹的名字 sudo：授权操作的许可,提升权限
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
netstat -ltnp // （Linux 服务器）
```

### 查看系统信息

```
uname -a
```

### 防火墙开放某个端口

```bash
# firewall-cmd --add-port=80/tcp　//即时打开，这里也可以是一个端口范围，如1000-2000/tcp
```

### 关闭防火墙

```bash
systemctl stop firewalld.service
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
# rm  test.txt
rm：是否删除 一般文件 "test.txt"? y
# rm  homework
rm: 无法删除目录"homework": 是一个目录
# rm  -r  homework
rm：是否删除 目录 "homework"? y
```

### Linux mv

英文全拼：move file）命令用来为文件或目录改名、或将文件或目录移入其它位置。

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

```
location / {
  try_files $uri $uri/ /index.html;
}
```

#### Apache

```
<IfModule mod_rewrite.c>
  RewriteEngine On
  RewriteBase /
  RewriteRule ^index\.html$ - [L]
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule . /index.html [L]
</IfModule>
```
