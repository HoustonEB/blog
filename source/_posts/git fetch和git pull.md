---
title: git fetch 和 git pull
date: 2019-09-17 19:26:37
categories: Git
tags:
- Git
---
### 区别
`git fetch`和`git pull`都是同步远端的代码,区别是前者将远端的更新全部更新到本地git远端文件夹(remotes)内,不会自动merge.
![1.png](1.png)
后者即会更新本地远端文件夹,也会合并到本地当前分支.
![d](2.png)
### 用法
1. git fetch
```bash
git fetch origin master // 拉取远程主机的master分支最新内容
git log -p FETCH_HEAD // 查看拉取的信息
git merge FETCH_HEAD // 合并fetch最新的内容到当前分支
```
2. git pull
```bash
git pull 远程主机名 远程分支名:本地分支名 // eg: git pull origin master:dev
```
