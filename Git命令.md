# Git 全局设置:

---

-   基本设置

```bash
git config --global user.name "jinyanhong"
git config --global user.email "820877998@qq.com"
```

-   创建 SSH 密钥

```bash
cat ~/.ssh/id_rsa.pub
ssh-keygen -t rsa -C "820877998@qq.com"
ssh -T git@code.aliyun.com
clip < ~/.ssh/id_rsa.pub
```

-   添加本地 SSH 配置

```bash
$ vim ~/.ssh/config
Host *
	HostkeyAlgorithms +ssh-rsa
	PubkeyAcceptedKeyTypes +ssh-rsa
```

-   创建 git 仓库

```bash
git push --set-upstream origin master
git push -u origin master
# 已有仓库

cd existing_git_repo
git push --set-upstream origin master
#gitee.com
git remote add origin https:
#xxx
#xxx.git
# 推送 并关联 远程本地
git push -u origin(远程分支) master(本地分支)
```

# 版本控制

---

-   回撤到某一版本**(本地)**

```bash
# hard 销毁本地更改 soft 保留本地更改
git reset --hard cedc856 (commit Hash 字符串前 7 位)
git push --force origin master
git checkout 9ae2c2ce4ad80c87615965f8036fe01c661e646b（切换到以往版本）
```

-   查看当前 commit ID

```bash
# 获取完整
git rev-parse HEAD
# 获取简短commit
git rev-parse --short HEAD
```

-   切换到最新版本

```bash
git checkout master
```

# 本地仓库更改

---

-   **撤销本地更改**

```bash
# 文件名
git checkout .
```

-   撤销 commit（本地）

```bash
# 保留本地未提交更改
git reset --soft HEAD^

# 不保留本地更改
git reset --hard HEAD^
```

-   **修改本地 commit 消息**

```bash
git commit --amend
```

-   **图形化显示 git log 记录**

```bash
git log --graph --pretty=format:'%C(red)%h%Creset - %C(white)%s %C(yellow)%d %C(cyan)（%cr）%Creset %C(green)<%an> '
```

# Git Tag

---

## Tag 的添加：

-   创建本地 tag

```bash
git tag <tagName>
```

-   推送到远程仓库 --**( 单个 Tag 的推送)**

```bash
git push origin <tagName>
```

-   一次性推送所有 Tag

```bash
git push origin --tags
```

## Tag 的清除：

-   删除本地的 Tag

```bash
git tag -d <tagName>
```

-   远程 tag 的删除

```bash
git push origin :<tagName>
```

## 其他 Tag 命令

-   指定 Tag 信息

```bash
git tag -a <tagname> -m "XXX..."
```

-   切换标签

```bash
git checkout [tagname]
```

# Git Branch

-   **新建并切换分支**

```bash
git checkout -b branchName
```

-   **关联到远程分支**

```bash
git branch --set-upstream-to origin
```

-   **删除本地分支**

```bash
git branch -d branch_name
```

-   **删除远程分支**

```bash
# 删除远程分支
git branch -r -d origin branch-name

# 推送到远端
git push origin :branch-name
```
