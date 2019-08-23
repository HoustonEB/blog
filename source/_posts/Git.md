---
title: Git
date: 2019-08-22 11:38:16
categories: Git
tags: Git
---
## 常用git命令
1. 清除git缓存,添加新的文件进入暂存区
`git rm -r --cached .`
`git add .`
{% note info %}
应用场景:
    - 先暂存文件,没有git ignore文件
    - 将项目里的第三方git仓库化为己有
{% endnote %}
2. 拉取remote分支,并在本地创建分支
`git checkout local-branch origin/remote-branch`
