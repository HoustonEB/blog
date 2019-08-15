---
title: hexo
date: 2019-08-13 15:41:22
tags: hexo
---
## 命令
1. 开启服务
```shell
hexo server
```
2. 生成新文章
```shell
hexo new 'your article name'
```
<!-- more -->
3. 生成打包文件
```shell
hexo generate
```
4. 清除打包文件
```shell
hexo clean
```
5. 部署blog
需要配置_config.yml
```shell
hexo deploy
```
6. 生成新html
```shell
hexo new page 'your html name'
```
## 标签
1. 链接
```shell 
{% link [text] [url] [external] [title] %}
```
2. 图片
```shell
{% asset_img  fullimage fiddler1.jpg image %}
```
**hexo参考docs**
 - {% link hexo https://hexo.io/zh-cn/docs/tag-plugins.html %}
 - {% link next主题 http://theme-next.iissnan.com/theme-settings.html %}
 - {% link 第三方插件 https://anoyer.cn/article/Hexo%20%E5%85%A5%E9%97%A8%E6%95%99%E7%A8%8B.html %}