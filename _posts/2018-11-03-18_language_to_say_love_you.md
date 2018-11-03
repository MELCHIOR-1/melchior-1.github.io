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

可以看出，babel是为了解决多语言排版问题的宏包。这个包的名字也很有意思，babel在圣经中指巴别塔，《圣经·旧约·创世记》第11章记载，当时人类联合起来兴建希望能通往天堂的高塔（巴别塔）；为了阻止人类的计划，上帝让人类说不同的语言，使人类相互之间不能沟通，计划因此失败，人类自此各散东西。此事件，为世上出现不同语言和种族提供解释。

### 怎么在LaTeX中使用babel？
**废弃的方案：**

参考Dason Kurkiewicz的博客[using Jekyll and Mathjax](http://dasonk.github.io/blog/2012/10/09/Using-Jekyll-and-Mathjax/).

1、在```_config.yml```文件的markdown字段改为```markdown: redcarpet```，默认的是使用 kramdown。

2、在```_layouts```文件夹的```page.html```中，添加如下代码：
{% highlight r %}
<script type="text/javascript"
    src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
{% endhighlight %}

**新方案：**

在准备改```_config.yml```文件的时候，发现提示：'redcarpet' is unsupported on GitHub Pages now.

也就是说，要在github上使用，就必须使用 kramdown。在知乎上找到了一个满意的答案 [如何在基于jekyll的github上发布的博客中支持MathJax(LaTex数学公式)？](https://www.zhihu.com/question/62114522).

步骤很简单，在_includes/head.html （我使用的是NexT主题，对应的文件在_includes/_partials/head.html ）中添加如下代码：
```
<!-- 数学公式 -->
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
      inlineMath: [['$','$']]
    }
  });
</script>
```
### 如何使用？
使用方法跟写LaTeX一样。对于行内公式，使用```$\$...\$$```；对于需要单独成行的公式，使用```$\$\$...\$\$ $```。

如勾股定理：

$$ \alpha^2+\beta^2=\gamma^2 $$

其中，$\alpha, \beta, \gamma$为正实数。