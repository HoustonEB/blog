---
title: npm发包
date: 2019-08-21 14:00:36
categories: npm
tags: 
- npm
- npm发包
---
## 添加Change Log
1. **安装commitizen**
`npm install commitizen -g`
在你的项目里执行一下命令,进行初始化
`commitizen init cz-conventional-changelog --save-dev --save-exact`
{% label info@commitizen %}包的作用提供`git cz`命令代替`git commit -m `

{% asset_img add-commit.png %}
<!-- more -->
2. **安装conventional-changelog-cli**
`npm install -g conventional-changelog-cli`
进入你的项目并生成CHANGELOG.md文件
```shell
cd my-project
conventional-changelog -p angular -i CHANGELOG.md -s 生成最新一条的commit记录
```
 `conventional-changelog -p angular -i CHANGELOG.md -s -r 0` 生成以往全部的commit记录到changelog文件中
 {% label warning@会复写已存在的changelog.md文件 %}
 3. 推荐的工作流
 - 修改代码
 - commit changes
 - 确保持续集成成功
 - 提升package.json中包的版本
 - 生成changelog记录(`npm run changelog`)
 - 提交package.json和changelog.md的改动
 - Tag
 - Push
 
 {% note primary %}
补充:
  {% label primary@在package.json中用别名执行命令 %}
  "changelog": "conventional-changelog -p angular -i CHANGELOG.md -s"
 {% endnote %}

