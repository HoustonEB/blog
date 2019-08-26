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
3. tag
**查看本地全部tag**
`git tag`
**给某个commit添加tag**
`git tag tagName commitHash`
**推动本地tag到远端**
`git push --tags origin`
**删除tag**
`git tag -d tagName`
**查看tag是在哪个commit打的**
`git show tagName`
