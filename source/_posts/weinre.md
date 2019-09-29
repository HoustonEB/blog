---
title: weinre
date: 2019-09-29 11:29:24
categories: 移动端调试工具
tags:
- weinre
- 移动端调试工具
---
## weinre是什么
weinre(Web Inspector Remote).是一种远程调试的工具,在电脑上可以调试手机远端的页面,包括样式,查看js变量和页面上的报警信息.
可以通过`document.body.style.color='red'`实时改变文字颜色.

## 工作原理
- 目标页面（target）：被调试的页面，页面已嵌入weinre的远程js，下文会介绍；
- Debug客户端（client）：本地的Web Inspector调试客户端；
- Debug服务端（agent）：一个HTTP Server，为目标页面与Debug客户端建立通信。

{% asset_img 1.png %}
<!-- more -->
## 用法
1. mac

```bash
// 安装
npm i -g weinre
// 开启服务
weinre --boundHost -all-
```
{% asset_img 2.jpg %}

## options
--help : 显示Weinre的Help
--httpPort   [portNumber] : 设置Weinre使用的端口号， 默认是8080
--boundHost  [hostname | ip address | -all-] : 默认是'localhost'， 这个参数是为了限制可以访问Weinre Server的设备， 设置为-all-或者指定ip， 那么任何设备都可以访问Weinre Server。
--verbose   [true | false] : 如果想看到更多的关于Weinre运行情况的输出， 那么可以设置这个选项为true， 默认为false；
--debug   [true | false] : 这个选项与--verbose类似， 会输出更多的信息。默认为false。
--readTimeout   [seconds] : Server发送信息到Target/Client的超时时间， 默认为5s。
--deathTimeout   [seconds] : 默认为3倍的readTimeout， 如果页面超过这个时间都没有任何响应， 那么就会断开连接。

### 相关链接
[weinre文档](https://github.com/nupthale/weinre)