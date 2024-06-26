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

### 金斧头还是银斧头

在线markdown编辑器，有几种形式：
1、自带后台，提供账户存储，比如一些笔记软件（为知笔记、石墨等），这种在线编辑markdown确实比较方便，但同步到github上，就需要比较麻烦的操作了；另外，总感觉如果只是写博客，用这些笔记类的软件，有点大材小用。
2、不带后台，数据直接存储在浏览器storage中，比如[StackEdit](https://stackedit.io/app#)、[doocs.md](https://github.com/doocs/md)、[Editor.md](https://pandao.github.io/editor.md/en.html)，其中StackEdit可以直接同步github的文章，doocs.md能很方便地排版成微信公众号文章，Editor.md是个功能强大的编辑器，可以嵌入公式、流程图、还可以写PPT，甚至它本身也可以嵌入网页中，作为一个嵌入式的markdown编辑器。
由于博客主要挂在github上，所以个人偏向于用StackEditor，但StackEdit有个问题，没法添加图床，后面等插图用的多了再说吧，可能需要再找一个解决插图的工具吧。
3、基于github的开源在线markdown编辑器，自己二次开发一套适配的markdown编辑器，但考虑到这是个不小的工程，还是先不考虑了。

### 先动手吧
在《精力管理》里面有句话：
> 人们总是高估一天能完成的事，而低估30天能完成的事。

先动手写起来吧。

> Written with [StackEdit](https://stackedit.io/).

<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IOS9v+eUqHN0YWNrZWRpdG
9yLmlv5Zyo57q/57yW6L6RZ2l0aHVi5Y2a5a6iXG5hdXRob3I6
IHNoYXdwYW5cbnRhZ3M6ICdyZXNvdXJjZXMsamVreWxsJ1xuY2
F0ZWdvcmllczogSlNcbmRhdGU6ICcyMDI0LTA1LTE5J1xuZXh0
ZW5zaW9uczpcbiAgcHJlc2V0OiBnZm1cbiIsImhpc3RvcnkiOl
syMDk5OTY4NjExLDE4MDQ2NjY0NzYsLTQ2NjgzMzk5LDEyOTU2
MTg4NDEsLTY3NjQwNTQxNiw4NTAyMzU1MywyMTI3MzA0NjI1LD
E4MDM4NTc4NzBdfQ==
-->