---
title: git reset和git revert
date: 2019-09-17 20:04:58
categories: Git
tags:
- Git
---
1. get reset
回退到指定版本,提交历史中看不到指定版本后的提交历史.
```bash
git reset --hard 版本号
```
2. git revert
反转指定版本的修改,回生成新的revert的commit历史信息.
```bash
git revert 版本号
```

