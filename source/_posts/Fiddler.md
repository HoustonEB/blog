---
title: Fiddler
date: 2019-05-06 17:11:23
categories: 抓包
tags: 
- 抓包
---
### 安装
---
1. windows:
- 无脑下一步.

2. mac:
- [下载fiddler](https://www.telerik.com/download/fiddler/fiddler-osx-beta)
- 下载fiddler运行的环境[mono下载](http://www.mono-project.com/download/#download-mac)
- 下载证书用于fiddler访问https协议的请求
`/Library/Frameworks/Mono.framework/Versions/<Mono Version>/bin/mozroots --import --sync` 
**mac环境下Library路径在user的上级, 不是个人users下的Library**
- 将mono加入全局环境变量中`sudo vi ~/.bash_profile`, 并写入
`export MONO_HOME=/Library/Frameworks/Mono.framework/Versions/5.4.1`
`export PATH=$PATH:$MONO_HOME/bin`
- cd到对应的fiddler解压后的文件夹里,运行32位的fiddler`mono --arch=32 Fiddler.exe`
**<Mono Version>mono版本取前三位**

### 使用
---
{% asset_img fiddler1.jpg image %}
{% asset_img fiddler2.jpg image %}
fiddler要代理手机上的请求需满足
- 代理地址需要填pc的ip地址`ifconfig`端口号是8888.
- 手机和pc要再同一个网下.
{% asset_img fiddler3.jpg image %}