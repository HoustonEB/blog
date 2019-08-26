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
 - 提升package.json中包的版本 {% label warning@利用npm version 更改版本 %}
 - 生成changelog记录(`npm run changelog`)
 - 提交package.json和changelog.md的改动
 - Push
 
**npm version**
npm version prepatch的作用: 1.修改预备修订版的版本号 2.生成tag
生成changelog会根据tag生成多条记录
0.0.1-1 => 主版本号.此版本号.修订号-预发布号

 npm version | 功能 
 :-: | - 
 major | 主版本号 <br/>- 如果没有预发布号: <br/>1.直接升级一位大号，其他位都置为0<br/>- 如果有预发布号: <br/>1.中号和小号都为0,则不升级大号,而将预发布号删掉.即2.0.0-1变成2.0.0,这就是预发布的作用<br/>2.如果中号和小号有任意一个不是0,那边会升级一位大号,其他位都置为0，清空预发布号.即 2.0.1-0变成3.0.0
 premajor | 预备主版本 <br/>- 直接升级大号，中号和小号置为0，增加预发布号为0
 minor | 次版本号 <br/>- 如果没有预发布号: <br/>1.升级一位中号，大号不动，小号置为空<br/>- 如果有预发布号: <br/>1. 如果小号为0，则不升级中号，将预发布号去掉<br/>2. 如果小号不为0，同理没有预发布号
 preminor | 预备次版本 <br/>- 直接升级此版本号,增加预发布号为0
 patch | 修订号 <br/>- 如果没有预发布号: 升级修订号,去掉预发布号<br/>- 如果有预发布号: 去掉预发布号,其它不动
 prepatch | 预备修订版 <br/>- 直接升级修订号, 增加预发布号为0
 prerelease | 预发布版本 <br/>- 如果没有预发布号: 升级修订号,预发布号为0<br/>- 如果有预发布号: 升级预发布号
 
 {% note primary %}
补充:
  {% label primary@在package.json中用别名执行命令 %}
  "changelog": "conventional-changelog -p angular -i CHANGELOG.md -s"
 {% endnote %}

