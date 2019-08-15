---
title: charles
date: 2019-08-15 15:14:48
tags: charles
categories: 抓包工具
---
{% note info %}
charles常用技巧
{% endnote %}
1. 断点mock数据
右键你需要打断点的请求.
<!-- more -->
{% asset_img charles4.jpg %}
刷新页面后可以编辑发出的请求和修改响应的数据.

{% asset_img charles5.jpg %}

------

{% note warning %}
使用charles经常会遇到的问题总结:
{% endnote %}
1. 抓不到https请求
安装证书.

{% asset_img charles1.jpg %}
开启SSL代理,监听所有host和port.

{% asset_img charles2.jpg %}
2. 请求没有被charles代理成功.
将本地的http和https代理到本机ip地址,port是charles的默认端口号8888

{% asset_img charles3.jpg %}
    
