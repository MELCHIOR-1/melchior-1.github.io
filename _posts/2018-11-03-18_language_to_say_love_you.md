---
layout: post
title: "用17+1种语言说我爱你之latex版"
date: 2018-11-03
categories: latex
tags: [babel, latex]
lang: zh
---

最近一直在想用什么例子来讲如何编写latex模板，老感觉使用“Hello World”或者“Hello LaTeX”就落入了市面上介绍编程语言的俗套。恰逢老婆生日，于是便有了用17种语言说“我爱你”作为例子的想法。

为什么是17种语言？哈哈，在室里读博读久了，脑海里就会冒出千奇百怪的问题，高晓松导演的电影《那时花开》里面朴树教周迅用17种语言说我爱你。

为什么最后又加了一种语言？最后一种为克林贡语，作为《星际迷航》迷，这个必须得安利一下，哈哈。

<!--more-->

要完成这个例子，首先需要引入一个非常重要的包——babel。

### 什么是babel？

在[CTAN](https://www.ctan.org/pkg/babel)上是这样描述它的：

> This package manages culturally-determined typographical (and other) rules for a wide range of languages. A document may select a single language to be supported, or it may select several, in which case the document may switch from one language to another in a variety of ways.

可以看出，babel是为了解决多语言排版问题的宏包。这个包的名字也很有意思，babel也有巴别塔之意，《圣经·旧约·创世记》第11章记载，当时人类联合起来兴建希望能通往天堂的高塔（巴别塔）；为了阻止人类的计划，上帝让人类说不同的语言，使人类相互之间不能沟通，计划因此失败，人类自此各散东西。此事件，为世上出现不同语言和种族提供解释。

### 怎么在LaTeX中使用babel？

在导言区添加babel包，并指明使用的语言。

如使用俄语写作，在导言区添加如下语句：
```latex
\usepackage[russian]{babel}
```

当然，你若就这样开始写俄文了，可能会遇到两个坑。

- 如果习惯用pdfLaTeX编译，编译就会出错。因为babel要求使用Unicode引擎（XeLaTeX或者LuaLaTeX）编译，毕竟unicode基本上包含了所有的语言编码。
- 使用XeLaTeX或LuaLaTeX编译，编译能顺利完成，但是生成的pdf是一片空白或者一片框框。是不是有种茶壶里煮饺子的感觉？怎么办？换口锅来煮饺子呗。实际上，这是由于默认的字体对俄语不支持导致的。在babel官方文档里面，推荐使用```DejaVu Serif
```字体，笔者发现```CMU Serif```也可以。

所以，在导言区添加如下代码：
```latex
\usepackage[russian]{babel}
\usepackage{fontspec}
\setmainfont{CMU Serif}
```
然后，使用XeLaTeX或LuaLaTeX编译，就可以了。

### 说好的17+1种语言说我爱你呢？
对于一个需要使用多种语言的文档，可以在引入babel包时申明使用哪些语言，如俄语和英语：
```latex
\usepackage[russian,english]{babel}
```
babel会把最后一个申明的语言当成主语言（如上例中的english），或者也可以显式的指明主语言，如：
```latex
\usepackage[main=russian,english]{babel}
```
或许你会问，为什么要申明主语言呢？这主要跟caption、date等宏的编译显示有关。比如english是主语言的话，那么你在图片环境里面输入```\caption{test}```，编译出来的就是```Figure.X test```；而主语言是俄语，编译出来就是```диаграмма.X test```。

好了，万事俱备，只欠东风了。现场自己把“我爱你”翻译成各种语言是不可能了，就只能借助于度娘了。
完整的源码如下：
```latex
\documentclass[a4paper,UTF8]{ctexbook}
\usepackage[french,german,czech,danish,finnish,dutch,greek,russian,icelandic,irish,latin,japanese,malay,polish,romanian,english]{babel}
\usepackage{fontspec}
\setmainfont{CMU Serif}
\begin{document}
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
\end{document}
```

在win10平台下，预装texlive2017，使用XeLaTeX编译，结果如下：
![](http://github.com/MELCHIOR-1/melchior-1.github.io/raw/master/images/18language.png)

### 参考资料
- [babel.pdf](ftp://ftp.dante.de/tex-archive/language/babel/base/babel.pdf)
- [克林贡人的爱意](https://www.douban.com/group/topic/52907756/)