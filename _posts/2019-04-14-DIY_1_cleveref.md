---
layout: post
title: "自己动手写LaTeX模版系列（四）——那些年你多写的图表"
date: 2019-04-14
categories: LaTeX
tags: [sty,latex]
lang: zh
---

种一棵树最好的时间是十年前，其次是现在。只要你心里有信念，没有时间的差距，什么时候开始都可以。——Dambisa Moyo

<!--more-->

LaTeX一个迷人的优点就是引用非常智能，不会出现“错误！未找到引用源”（Word的老梗）。

虽然解决了引用关联的问题，但是仍有2处让人感觉比较繁琐。

1、每次引用的时候，需要写“图\~\ref{}”或“表\~\ref{}”。写小论文还要好点，顶多多写几十个“图\~”或“表\~” (Figure\~ or Table\~)；轮到写大论文可就惨了，图、表、公式加起来可能有几百个了吧。

2、在写英文论文时，有的期刊要求使用“Figure”，而有些则使用“Fig.”，表格和公式也是如此；在写中文论文时，也会遇到“式(1)”和“(1)式”的纠结。



### 是痛点吗？

在工作中，逐渐学会了在做一件事情前先进行价值和难度的评估。即做这件事情的价值大吗（不做会死吗，做成了会带来多大的收益）？做件事的时间和人力成本有多大？

但经常这样思考，会容易让人陷入一个短视和功利的状态。有些事情，在短期看来，费时又没有带来多大的收益，但如果把眼光放长，会发现这些事情正在潜移默化地改变着我们，长期收益要远大于短期收益。

用LaTeX写作就是一个长期收益要远大于短期收益的事情。大论文不用LaTeX写可以吗？完全可以的，用word一样可以丝溜润滑；那用LaTeX写价值大吗？有人会说LaTeX排版功能很强大，改格式很方便，但是君不知为了搞清楚怎么改格式可能会花费跟在word中傻瓜式重复修改更多的时间。再说了，万一格式要求今年没有变化呢？大论文一气呵成写完了呢？

道理上要做一劳永逸的事情，但一劳永逸的事情是否都值得我们去做？相信大家心里面都有一杆秤。公园的门票，年票比单次票可能就贵一点，你会去买年票吗？

### 不痛还做吗？

在LaTeX中，有多种宏包可以帮咋们做这件事，如：cleveref, varioref, fancyref和hyberref宏包的\autoref命令等。这里面功能最全最新的要数cleveref，在一篇论文里也可以同时使用多个宏包。

```latex
\usepackage{varioref}
\usepackage{hyperref}
\usepackage{cleveref}
```

这里注意的是：hyberref需要在cleveref宏包前加载。



接下来，主要讲一下cleveref宏包的用法。



### 怎么引用？

不管你是图片引用，还是公式引用，只需要使用\cref{}就可以，剩下的就交给程序去识别，进而输出"fig. XX"或"eq.(XX)"。来段代码感受一下。

```latex
\documentclass[11pt]{article}
\usepackage{cleveref}
\begin{document} 
\begin{equation}
	y=a_1x+b_1\label{eqn:1}
\end{equation} 

Cleveref equation reference (\textbackslash cref): \cref{eqn:1}.
\begin{figure}[ht]
	\centering
	\rule{0.5\linewidth}{0.1\linewidth}
	\caption{First figure}\label{fig:1}
\end{figure}

Cleveref figure reference (\textbackslash cref): \cref{fig:1}.
\end{document}
```

编译一下，如下图所示：

![](<https://github.com/MELCHIOR-1/melchior-1.github.io/raw/master/images/cleveref_first.png>)



### 搞定了吗？

相信聪明如你，一眼就可以看出这个例子太简单，实际使用中还会遇到很多问题需要解决，比如：

- 如果引用是在句首，需要首字母大写怎么办？

此时，需要使用\Cref{}，该命令出来的引用首字母会大写。

```latex
\Cref{eqn:1} is a normal linear equation.
```

- 如果所有的引用首字母都需要大写怎么办？

此时，在导言区加载cleveref宏包时添加[capitalise]选项。

```latex
\usepackage[capitalise]{cleveref}
```

- 如果要引用多个公式（或图片）怎么办？

分两种情况：

1、当引用的公式不连着，可以把公式的label直接按顺序写到\cref{}里面，中间用逗号隔开，不要加空格。

```latex
\cref{eqn:1,eqn:3,eqn:7}
```

2、当引用的公式连着，有个简单的办法，使用\crefrange{first}{last}，first中填第一个公式的label，last中填最后一个公式的label。如需要引用公式1-7：

```latex
\crefrange{eqn:1}{eqn:7}
```

- 如果公式和图要混合引用怎么办？

作为cref的开发者，势必会把这种情况最为检测cleveref宏包智能性如何的一个测试用例，你可以试试如下语句：

```latex
\cref{eqn:1,fig:1}
```

- 如果引用时需要全称而不是缩写怎么办？

此时，需要在导言区加载cleveref宏包时添加[noabbrev]选项。

```latex
\usepackage[noabbrev]{cleveref}
```

- 如果要定制引用标签怎么办？

先解释一下这个问题产生的场景。比如我们需要把引用写成这样子——"fig-X"或"fig: X"；来个更实际的，比如在写大论文时，我们使用的都是"图 X"和"式 (X)"，而对于cleveref，目前还不能根据使用的主语言来输出对应引用标签。什么意思？就是你在ctex环境下，输入的全是中文，使用\cref{fig:1}默认输出的还是fig. 1而不是图1。

这时候自定义设置就派上用场了。在导言区添加如下设置：

```latex
\crefname{equation}{equation}{equations}
```

在命令`\crefname{·}{·}{·}`中的第一个参数的含义是引用的类型（equation、table、figure、section等），第二个参数包含的单词，当只有一个引用时将会被输出，当有多个引用是第三个参数将会被输出。在中文情况下：第二个参数和第三个参数可以是汉字，如：`\crefname{equation}{式}{式}`。

- 如果想要点一下引用就跳转到引用源的位置怎么办？如点击"图 1"就可以跳转到图片1的位置？

这个功能就属于hyperref的范围了，cleveref能够很好的兼容hyperref，只要添加hyperref宏包就可以了，但是注意，一定要在cleveref之前添加hyperref宏包。

```latex
\usepackage{hyperref}
\usepackage{cleveref}
```

### 怎么写到模版里？

我们在demo_style.sty中添加如下代码：

```latex
\RequirePackage{graphicx}
\RequirePackage[colorlinks=true,linkcolor=black]{hyperref} 
\RequirePackage{cleveref}
\crefname{equation}{式}{式}
\crefname{table}{表}{表}
\crefname{figure}{图}{图}
```

然后，新建一个tex文档`use_cleveref.tex`，输入如下代码：

```latex
\documentclass{thesis_demo}
\usepackage{demo_style}
\begin{document}
	如\cref{fig:wechat}所示，为cref的引用演示。
	\begin{figure}[!htbp]
		\centering
		\includegraphics[width=7.5cm]{wechat.jpg}
		\caption{微信图标}
		\label{fig:wechat}
	\end{figure} 
\end{document}
```

使用xelatex编译一下，可以生成如下结果：

![](<https://github.com/MELCHIOR-1/melchior-1.github.io/raw/master/images/cleveref_second.png>)



源码地址：

[https://github.com/MELCHIOR-1/How\_to\_write\_a\_LaTeX\_thesis\_template/tree/master/chapter\_1/section5][https://github.com/MELCHIOR-1/How\_to\_write\_a\_LaTeX\_thesis\_template/tree/master/chapter\_1/section5]



