---
layout: post
title: "自己动手写LaTeX模版系列（二）——随手写个宏包"
date: 2018-11-24
categories: LaTeX
tags: [sty,latex]
lang: zh
---

“你在北方的寒夜里 大雪纷飞
我在南方的艳阳里 四季如春” 

冲之大道路旁的异木棉开花了，为绿色的冬季增添了点点鲜红。你呢？飘落的银杏是否铺成了金黄的冬季。

<!--more-->

上篇文章讲了LaTeX类文件的写法，这篇文章就来介绍一下宏包的写法。

### 什么是宏包？

LaTeX模版包括两个部分：类 (.cls) 和 包 (.sty)。类就好比是皮囊，包就是衣服。俗言道：人靠衣装。一件合适的衣服，可以完美的彰显一个人的气质和内涵，说白了，就是有的衣服显高，有的衣服显瘦。

### 如何编写宏包？

编写宏包和编写类文件非常相似。也分4步。

- 申明生产厂家: ```\NeedsTeXFormat{LaTeX2e}[1995/12/01]```
- 标明名称和出厂日期: ```\ProvidesPackage{<package>}[date]```
- 有什么功能: ```\DeclareOption{<option>}{<code>}```
- 用的是什么面料: ```\RequirePackage[<options>]{<package>}[<date>]```

实战一下，同样配合《17+1种语言说我爱你》的例子，新建一个```thesis_demo.sty```文件，用来让TeX编译出的文件显示特定的字体，填入如下内容：
```latex
\NeedsTeXFormat{LaTeX2e}[1995/12/01]
\ProvidesPackage{demo_style}[2018/11/11]
\DeclareOption*{\PackageWarning{demo_style}{Unknown option '\CurrentOption'}}
\ProcessOptions\relax
\RequirePackage{fontspec}
\setmainfont{CMU Serif}
```
注意上述代码的最后两行关于字体的设置，这两行本来是写在thesis_demo.cls类文件中，但写在宏包中更合适一些，因为换字体就像换衣服一样，只是外表变了。

### 怎么用宏包？

使用宏包也非常简单，在tex文件的导言区申明宏包，如：
```latex
\usepackage{demo_style}
```
来使用之前咋们新建的demo_style宏包。

### shapepar宏包

在实际写作中，我们大多都是采用别人的宏包（样式），TeXLive套装中也包含了很多有用的宏包。介绍一个比较有意思的宏包——shapepar，这货能把正文包裹在一个特定的形状中。

举个栗子，咋们把18种语言的我爱你包裹在心形中。新建一个18_kinds_with_style.tex文件，填入如下代码：
```latex
\documentclass{thesis_demo}
\usepackage{demo_style}
\usepackage{shapepar}
\begin{document}
	\heartpar{
	\textbf{汉语：}我爱你！
	\textbf{英语：}I love you.
	\textbf{俄语：}Я люблю тебя. 	
	\textbf{日语：}あなたのことが好きです.
	\textbf{法语：}Je t'aime!
	\textbf{德语：}Ich liebe dich.
	\textbf{荷兰语：}Ik hou van je.
	\textbf{捷克语：}miluju tě.
	\textbf{丹麦语：}jeg elsker dig.
	\textbf{芬兰语：}rakastan sinua.
	\textbf{希腊语：}σ 'αγαπώ.
	\textbf{冰岛语：}Ég elska þig.
	\textbf{波兰语：}Kocham cię.
	\textbf{拉丁语：}Te amo.
	\textbf{马来语：}Saya sayang awak.
	\textbf{爱尔兰语：}Is breá liom tú.
	\textbf{罗马尼亚语：}Te iubesc.
	\textbf{克林贡语：}qamuSHa'.
	}
\end{document}
```
使用XeLaTeX编译后，可以得到如下效果：
