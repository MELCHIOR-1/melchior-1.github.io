---
layout: post
title: "自己动手写LaTeX模版系列（一）——最小模版"
date: 2018-11-11
categories: LaTeX
tags: [latex]
lang: zh
---

“孤单是一个人的狂欢,狂欢是一群人的孤单。” ——阿桑《叶子》

双十一到了，你是一个人在狂欢，还是跟着一群人在孤单？

<!--more-->

上篇文章说道，我们将拿```18_kinds_of_language_to_say_love_you.tex```借尸还魂，生成一个最小模版。

### 为什么要模版？

就好像面向对象的编程语言里面，需要类一样。使用类可以大大简化操作和使用，还可以使编程时思路更清晰、更有条理性。

说了这么多虚的，似乎没有什么用。作为程序猿，信奉的是 “Talk is cheap, show me your code”! 下面就开始说干货了。


### 模版是什么？

LaTeX模版包括两个部分：类 (.cls) 和 包 (.sty)。类就好比是皮囊，包就是衣服，衣服可以不穿，但皮囊一定得披。

俗言道，“好看的皮囊千篇一律”。LaTeX模版也是这样，不信你可以去看看那些漂亮的模版，比如IEEE期刊的、iecas_thesis的（哈哈，王婆卖瓜，自卖自夸），在结构、套路上都如出一辙。

那么，怎么才能拥有一个好的皮囊呢？最好的方法就是出生时拥有一个好的胚子。接下来我们就来制造这个美人胚子。

### 模版的要素

1、父母是谁？

每个小生命，都是从父母身上脱胎换骨而来，保存着父母优良的基因。有时候，我们看一个小孩有多大的潜力，将来可能在哪个方面有所作为，可以看他的父母是谁。现实中的例子也比比皆是，如上海某幼儿园入学需要面试父母。古语道，“龙生龙，凤生凤，老鼠的孩子会打洞”。当然，任何事情都需要用辩证的眼光去看待，“龙生九子，子子不同”，更何况我们都是龙的传人。

在类文件（.cls）的开头，首先声明父母是谁，即你基于的LaTeX版本。
```latex
\NeedsTeXFormat{LaTeX2e}[1995/12/01]
```

2、姓名和出生日期

就像一个刚出生的小生命，作为一个单独的个体，父母都会给他起一个好听的名字，这个名字里面寄托了父母对他的期望。所以一个美人胚子一定要有一个好听的名字。出生日期，对于每一个个体也非常重要，它决定了你的生辰八字，古时候相亲，都要看两个人的八字合不合。

在申明父母后，就要申明这个类的名字和出生日期，假设我们的类叫做```thesis_demo```，则作如下申明。
```latex
\ProvidesClass{thesis_demo}[2018/11/11 v0.1 LaTeX document class]
```
今天这个生日有点尴尬哈。

3、有什么特点？

一个好胚子一般就有良好的可塑性，如它可以长成单眼皮或者双眼皮、浓眉或秀眉。对于模版来说，就是我们可以指定一些参数，使通过模版编译的文档呈现出我们想要的样子。当然，首先模版得具备这样的能力。

在LaTeX模版中，通过```\DeclareOption{<option>}{<code>}```来实现这样的功能。如：
```latex
\DeclareOption{a4paper}{
\setlength{\paperheight}{297mm}
\setlength{\paperwidth}{210mm}
}
```

还有一个偷懒的方法，就是找一个网红胚子，一样的特点就直接调用网红胚子的，不一样的特点在自己单独造（有点像继承）。如我们使用```ctexbook```类作为底胚。
```latex
% Handle non-implemented options
\DeclareOption*{
    \PassOptionsToClass{\CurrentOption}{ctexbook}
}
```
申明完特点后，要告诉编译器特点说完了，可以放松一下。
```latex
% Terminates all options processing
\ProcessOptions\relax
```

4、社会关系

人在江湖，父母只给了皮囊，人在江湖，要习得一身武艺，还得靠拜师学艺，所以师父很重要。要学成哪门武功，就要拜哪门子的师父。在LaTeX模版中，通过```\LoadClass[<options>]{<class-name>}[<date>]```对某个类拜师，通过```\RequirePackage[<options>]{<package>}[<date>]```对某个包拜师，其中```options```中申明你要学的武功。

### 怎么用？

一开始说过，要拿```18_kinds_of_language_to_say_love_you.tex```练手，其代码如下：
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

在同目录下新建一个```thesis_demo.cls```文件，插入如下代码：
```latex
\NeedsTeXFormat{LaTeX2e}[1995/12/01] % 申明父母
\ProvidesClass{thesis_demo}[2018/11/11 v0.1 LaTeX document class]% 申明名字和出生日期
\DeclareOption*{ % 引用特点
    \PassOptionsToClass{\CurrentOption}{ctexbook}
}
\ProcessOptions\relax %  终止特点描述
\LoadClass[UTF8,a4paper]{ctexbook} % 拜师ctexbook
\RequirePackage[french,german,czech,danish,finnish,dutch,greek,russian,icelandic,irish,latin,japanese,malay,polish,romanian,english]{babel}% 拜师babel
\RequirePackage{fontspec} %	拜师fontspec
\setmainfont{CMU Serif}
```
好了，第一个模版写好了，可以直接使用它了，新建一个tex文件```18_kinds_with_template.tex```，输入如下代码：
```latex
\documentclass{thesis_demo}
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
保存，然后使用XeLaTeX编译该文件，可以得到如下结果：
![](http://github.com/MELCHIOR-1/melchior-1.github.io/raw/master/images/18language.png)

对比```18_kinds_of_language_to_say_love_you.tex```和```18_kinds_with_template.tex```，可以看出，前者导言区里面的内容已经全部放到```thesis_demo.cls```，后者只需要引用```thesis_demo```类即可。

### 下篇预告

有了好看的皮囊，还需要搭配合适的衣裳。常言道，“人靠衣装”。一个功能强大的模版，不仅要有类，还需要相应的包。下篇中，我将讲解如何为一个类量身定制一个包，以及如何使用合适的包使你的latex文档更好看。

### 参考资料

- [clsguide_chs.pdf](https://wenku.baidu.com/view/a7a25a8371fe910ef12df8c9.html)