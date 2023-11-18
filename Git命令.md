## Git 全局设置:

### 基本设置

```bash
git config --global user.name "Jin-Yanhong"
git config --global user.email "820877998@qq.com"
```

### 创建并拷贝 SSH 密钥

```bash
ssh-keygen -t rsa -C "820877998@qq.com"

ssh -T git@github.com

# Linux 下
cat ~/.ssh/id_rsa.pub

# Windows 下
clip < ~/.ssh/id_rsa.pub
```

### 添加本地 SSH 配置

```bash
$ vim ~/.ssh/config
Host *
	HostkeyAlgorithms +ssh-rsa
	PubkeyAcceptedKeyTypes +ssh-rsa
```

### 创建 git 仓库

```bash
# 推送 并关联 远程本地
git push --set-upstream origin master
# 简写
git push -u origin master

# 已有仓库
cd existing_git_repo
git push --set-upstream origin master

# 添加远程分支
git remote add origin https:xxx.xxx.git
```

## 版本控制

### 回撤到某一版本(本地)

```bash
# 保留本地未提交更改
git reset --soft HEAD^

# 不保留本地更改
git reset --hard HEAD^

# 上两个版本
git reset --hard HEAD^^

# 上20个版本
git reset --hard HEAD~20

# 回退到指定commitID版本
git reset --hard cedc856 (commit Hash 字符串前 7 位)

# 强制提交
git push --force origin master

# 切换到以往版本
git checkout 9ae2c2ce4ad80c87615965f8036fe01c661e646b
```

## 本地仓库更改

### 撤销本地更改

```bash
# 文件名
git checkout .
```

### 切换分支前暂存本地

```bash
# 将改动存储到隐式存储并将改动的文件回滚到 HEAD 分支
git stash [push]

# 创建 隐式存储
git stash create "message"

# 将改动存储到隐式存储
git stash save

# 查看存储了哪些些文件
git stash show

# 查看有哪些隐式存储入口
git stash list

# 将第 index 个隐式存储应用于当前分支
git stash apply index

# 将第 0 个隐式存储应用于当前分支后删除
git stash pop

# 将第 index 个隐式存储删除
git stash drop index

```

### 修改本地 commit 消息

```bash
git commit --amend
```

#### 切换到本地最新版

```bash
git checkout master
```

## Git Tag

### Tag 的添加：

#### 创建本地 tag

```bash
git tag <tagName>
```

#### 推送到远程仓库

##### 单个 Tag 的推送

```bash
git push origin <tagName>
```

##### 一次性推送所有 Tag

```bash
git push origin --tags
```

### Tag 的清除：

#### 删除本地的 Tag

```bash
git tag -d <tagName>
```

#### 远程 tag 的删除

```bash
git push origin :<tagName>
```

### 其他 Tag 命令

#### 指定 Tag 信息

```bash
git tag -a <tagname> -m "XXX..."
```

#### 切换标签

```bash
git checkout [tagname]
```

## Git Branch

### 新建并切换分支

```bash
git checkout -b branchName
```

### 关联到远程分支

```bash
git branch --set-upstream-to origin
```

### 删除本地分支

```bash
git branch -d branch_name
```

### 删除远程分支

```bash
# 删除远程分支
git branch -r -d origin branch-name
git push origin --delete remoteBranchName

# 推送到远端
git push origin :branch-name
```

### 暂存工作区修改

```bash

```

## Git 查看相关信息

### 查看远程仓库的`url`地址

```bash
git remote get-url origin
```

### 图形化显示 git log 记录

```bash
git log --graph --pretty=format:'%C(red)%h%Creset - %C(white)%s %C(yellow)%d %C(cyan)（%cr）%Creset %C(green)<%an> '
```

### 查看当前 commit ID

```bash
# 获取完整
git rev-parse HEAD
# 获取简短commit
git rev-parse --short HEAD
```
