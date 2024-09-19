---
layout: post
title: "解决开机启动时不识别USB蓝牙的问题"
date: 2024-09-19
categories: others
tags: [win10, bugs]
lang: zh

---

最近使用蓝牙键盘，但是电脑一重启，键盘就打不了字了，排查了一下，是开机时不识别USB蓝牙的问题。
<!--more-->
在`https://zhuanlan.zhihu.com/p/450759260`知乎上找到了解决方案，由于遇到过几次，所以还是记录一下吧。

Windows 11台式机下使用USB蓝牙适配器，可能会在每次启动时插拔一次蓝牙适配器才可以正常使用。

解决方法为：

1.  运行services.msc。
2.  找到“蓝牙支持服务”和“蓝牙音频网关服务”。
3.  将这两个服务的启动类型设置为“自动（延迟）”。


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ3NjAwNzE0M119
-->