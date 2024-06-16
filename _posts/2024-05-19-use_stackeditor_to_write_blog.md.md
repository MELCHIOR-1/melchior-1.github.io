---
layout: post
title: "使用stackeditor.io在线编辑github博客"
date: 2024-05-19
categories: JS
tags: [resources, jekyll]
lang: zh
image: http://gastonsanchez.com/images/blog/mathjax_logo.png
---

最近一直在找一个不依赖系统、不依赖电脑的博客编辑方案，找到了这个网站。还不错，只是不支持github图床。
<!--more-->

### 磨刀不误砍柴工

俗话说，磨刀不误砍柴工。博客中断了6年，之前编辑博客的电脑也坏了，环境都没了，一些配置，一些用法，都不记得了，现在都需要重新拾起来。考虑到未来也可能会出现同样的状况，有些环境也会随日新月异的变化而过时，所以想用一个跟本地环境能解耦的方案，同时可以随时随地的登录编辑。

最直接的方法，就是直接编辑github上面的文件，还好之前用的是jekyll框架，markdown按照模板格式写完后，就能自动编译了，也不需要手动输入命令（之前一直担心需要自己编译，还看了一段时间github action实现自动化 :<）。

直接在github编辑markdown的最大缺陷在于不直观，没法实时渲染。所以找一个曲线救国的方法：找一款在线markdown编辑器，要么能在线存储文档，或者能及时同时能同步到github上，这样就能摆脱主机的限制、系统的限制。

在线markdown编辑器，有几种形式：1、自带后台，提供账户存储，比如一些笔记ru


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IOS9v+eUqHN0YWNrZWRpdG
9yLmlv5Zyo57q/57yW6L6RZ2l0aHVi5Y2a5a6iXG5hdXRob3I6
IHNoYXdwYW5cbnRhZ3M6ICdyZXNvdXJjZXMsamVreWxsJ1xuY2
F0ZWdvcmllczogSlNcbmRhdGU6ICcyMDI0LTA1LTE5J1xuZXh0
ZW5zaW9uczpcbiAgcHJlc2V0OiBnZm1cbiIsImhpc3RvcnkiOl
stMTU1NzU1NDQ0MiwtNjc2NDA1NDE2LDg1MDIzNTUzLDIxMjcz
MDQ2MjUsMTgwMzg1Nzg3MF19
-->