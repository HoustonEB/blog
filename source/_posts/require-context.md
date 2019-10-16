---
title: require.context()
date: 2019-10-16 10:28:52
categories: node
tags: 
- require.context
---
## require.context是什么

是webpack的api,通过执行require.context()函数获取一个特定的上下文,主要用来自动化导入模块,在前端工程中,如果遇到从一个文件引入很多模块的情况,可以使用这个api,它回遍历文件夹中的指定文件,然后自动导入,使得不需要每次显示的条用import导入模块.
<!-- more -->
## 用法

require.context接受三个参数
1. directory {String} -读取文件的路径
2. useSubdirectories {Boolean} -是否遍历文件的子目录
3. regExp {RegExp} -匹配文件的正则

```javascript
require.context('../../src/components', true, /\/_demo-normal\/index\.js$/)
```
require.context返回三个属性
1. resolve {Function} -接受一个参数request,request为components文件夹下面匹配文件的相对路径,返回这个匹配文件相对于整个工程的相对路径
2. keys {Function} -返回匹配成功模块的名字组成的数组
3. id {String} -执行环境的id,返回的是一个字符串,主要用在module.hot.accept,应该是热加载?
{% asset_img 2.jpg %}
{% asset_img 1.jpg %}
这个Module模块和使用import导入的模块是一样的

## 使用场景

1. 在demoModule中自动加载所有demo生成路由.
2. 使用svg