---
layout: post
title: "自己动手写LaTeX模版系列（三）——图表双标题"
date: 2018-12-18
categories: LaTeX
tags: [sty,latex]
lang: zh
---

“岁月是朵两生花，涉江而过，花开千朵” 

转眼间已经到年底了，离之前计划的目标还剩很远。思考了一下，决定改变写作策略。对于大论文写作来说，有些技巧是你在写作之前就需要掌握的，掌握了这些技巧，一是前期写作的时候能够事半功倍，二是后期减小通篇查找修改的成本；还有一些技巧是在你写作前后掌握都可以的，这类技巧主要是减小你修改格式的时间。所以，接下来我会优先讲解第一类技巧。

<!--more-->

上篇文章讲了LaTeX宏包的写法，实际上，大多数情况下我们都是在用各种各样的宏包。相信大家有了会写宏包的功底，各种宏包对于我们来说就不是黑盒子了，用好各种宏包也就不在话下。

IECAS采用UCAS的毕业论文格式要求后，较之前的论文模版有较大的变化，其中一个区别点就是新版使用了**双标题**。

### 什么是双标题？

这里所说的双标题是指在大论文写作中，图表的标题使用两种语言表述，比如IECAS的大论文，需要使用中英文标题，中文标题在上，英文标题在下。另外，在图表目录中，只显示中文标题。

有人会说，这个简单呀，每个Figure环境里面使用2次caption，在第二次使用caption前计数减1，然后在caption里面输英文就可以了呀。这样虽然解决了图表双标题显示的问题，但是图表目录中，又该如何只显示中文标题呢？对于编译系统来说，中英文都是使用的caption环境，本质上是一样的。

当然，把这些问题解决了，就可以自己编写一个双标题宏包了。根据懒人的思维，有没有人为我们做好了衣服，我们直接穿就行呢？

答案是肯定的，这个宏包就是bicaption，你的双标题解决方案。

### bicaption宏包是什么？

bicaption，从名字中可以看出，它是在caption的基础上实现了双语的功能。实际上，在LaTeX包的归档上，它属于caption宏包的一个子包，或者说是增强包。

### 怎么用bicaption宏包？

使用bicaption宏包也非常简单，接着之前的模版demo_style宏包，在里面添加bicaption宏包的引用。

```latex
\RequirePackage[list=off]{bicaption} % package for binary captions
\captionsetup[figure][bi-second]{name=Figure} % the second figure caption name
\captionsetup[table][bi-second]{name=Table} % the second table caption name
```
第一行代码申明了bicaption包的引用，其中```list=off```选项表示在图表目录中不显示第二语言标题。看，使用bicaption宏包，目录显示问题一条指令就能解决，是不是很方便？

这里其实引出了一个问题，使用LaTeX后，你可能都已经忘了图表标题编号的问题，因为LaTeX已经帮你处理好了，那么“图XX”中的“图”，或者“Figure XX”中的“Figure”是怎么处理的呢？

对于只有一种语言的文档，比如中文或英文，编译器可以根据class默认的语言来判断，如使用的是ctexbook类，编译出来默认就是“图XX”，而使用texbook类，默认的就是“Figure XX”。那么，对于两种语言的文档，编译器怎么去识别第二种语言呢？

没错，就是使用之前公众号文章中提到的多语言包————babel，在模版引用babel宏包时申明两种语言，前面一个是第二语言，后面一个是主语言，如：
```latex
\RequirePackage[russian,english]{babel}
```
第一语言申明是英语，第二语言是俄文。

那么，对于中英文标题（第一语言是中文，第二语言是英文），是不是使用```RequirePackage[english,pinyin]{babel}```就行了呢？

这样想就too young, too simple了，对于中文环境的完美适配，LaTeX还有一段路要走。引用刘海洋老师在《LaTeX入门》中提到的：

> bicaption原本使用babel或polyglossia提供的语言选择机制来设置不同的语言标题，不过中文等东亚语言不使用上述宏包的翻译机制，就需要手工设置不同的语言标题。


好了，现在问题变成了如何去设置第二语言标题？

上面代码的第二、三行便是对第二语言标题的设置，通过```\captionsetup[figure][bi-second]{name=Figure}```将英文图片标题设置为“Figure XX”。

如果你非常好奇，不设置会变成怎么样？亲测了一下，你的中英文标题都显示的是“图XX”。

环境准备好了，可以上手用了。在正文中，在本该使用caption的位置，替换成如下代码：
```latex
\bicaption{中文标题}{english title}
```

### 炒个栗子

按照惯例，举个例子。

先在demo_style.sty中添加对bicaption的设置。
```latex
\RequirePackage[list=off]{bicaption}% package for binary captions
\captionsetup[figure][bi-second]{name=Figure}% the second figure caption name
\captionsetup[table][bi-second]{name=Table}% the second table caption name
```

新建一个tex文件use_bicaption.tex，写入如下内容：
```latex
\documentclass{thesis_demo}
\usepackage{demo_style}
\usepackage{graphicx}

\begin{document}
	\listoffigures
	\newpage
	
	如图~\ref{fig:wechat}所示，为bicaption的标题演示。
	\begin{figure}[!htbp]
		\centering
		\includegraphics[width=7.5cm]{wechat.jpg}
		\bicaption{微信图标}{wechat icon}
		\label{fig:wechat}
	\end{figure} 
\end{document}
```
使用XeLaTeX编译后，可以得到如下效果：

【目录的效果】

![](https://github.com/MELCHIOR-1/melchior-1.github.io/raw/master/images/figure_index.png)

【标题的效果】
![](https://github.com/MELCHIOR-1/melchior-1.github.io/raw/master/images/bicaption_content.png)

源码地址：

[https://github.com/MELCHIOR-1/How_to_write_a_LaTeX_thesis_template/tree/master/chapter_1/section4](https://github.com/MELCHIOR-1/How_to_write_a_LaTeX_thesis_template/tree/master/chapter_1/section4)