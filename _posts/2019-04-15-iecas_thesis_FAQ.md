---
layout: post
title: "iecas_thesis FAQ（一）——子图中的括号"
date: 2019-04-15
categories: LaTeX
tags: [sty,latex]
lang: zh
---

使用模板时遇到了引用图像子图不带括号的问题。

<!--more-->

### 问题描述

在写论文时，会遇到一处图片有多个子图的情况。对于子图，可以使用subfigure宏包来处理，然后可以向添加图片一样添加子图。如果要引用子图，则需要在子图中添加标签，然后使用\ref{}来引用该标签。

如下图中，有4个子图，对于子图(a)，添加标签\label{fig:oaspl_a}，在正文引用时，使用\ref{fig:oaspl_a}。

![](<https://github.com/MELCHIOR-1/melchior-1.github.io/raw/master/images/FAQ_subfig_1.png>)

上图红框标出了问题所在：在引用单张图时，我们希望时"图 XX"，而在引用子图时，希望时"图 XX(a)"，为什么？因为上图中的子图标题就带有括号，这样引用显得一一对应。



### 解决方法

**step 1.**

为了解决这个问题，首先想到的就是改写thesubfigure命令。尝试在Thesis.tex的导言区中添加如下命令：

```latex
\renewcommand{\thesubfigure}{(\alph{subfigure})}
```

得到的效果是这样的：

![](<https://github.com/MELCHIOR-1/melchior-1.github.io/raw/master/images/FAQ_subfig_2.png>)

可以看到，虽然引用子图标号外面现在有括号了，但是大图中子图的标号也会多一层。



**step 2. **

查阅资料后发现在Thesis.tex的导言区中添加命令：

```latex
\usepackage[labelformat=simple]{subcaption}
```

即在加载subcaption宏包时添加[labelformat=simple]配置选项，就可以解决这个问题。编译结果如下：

![](<https://github.com/MELCHIOR-1/melchior-1.github.io/raw/master/images/FAQ_subfig_3.png>)

