---
title: npm命令
date: 2019-08-26 10:32:05
categories: npm
tags:
- npm
---
1. 查看npm全局安装的包
`npm list -g --depth 0`
2. root权限npm全局安装,仍会权限不足, --unsafe-perm
`sudo npm install --unsafe-perm=true`
3. 更新包
`npm update`更新全部包(慎用)
`npm update 包名`更新某个包名
`npm update 包名 -g`更新全局的某个包
也可以用install更新包`npm i name@版本号`
4. package.json中^ ~的区别
 - 比如"classnames": "2.2.5"，表示安装2.2.5的版本
 - 比如 "babel-plugin-import": "~1.1.0",表示安装1.1.x的最新版本（不低于1.1.0），但是不安装1.2.x，也就是说安装时不改变大版本号和次要版本号
 - 比如 "antd": "^3.1.4",，表示安装3.1.4及以上的版本，但是不安装4.0.0，也就是说安装时不改变大版本号。
5. 查看npmjs服务器上包的版本信息
```bash
npm view react versions；这种方式可以查看npm服务器上所有的react版本信息；
npm view react version； 这种方式只能查看react的最新的版本是哪一个；
npm info react 这种方式和第一种类似，也可以查看react所有的版本，但是能查出更多的关于react的信息；

2、查看本地已经安装的包的版本信息：
npm ls react （查看某个项目安装的react），命令必须在某个项目下执行
npm ls react -g (查看全局安装的react)
```