---
layout: post
title: 精简Mathjax
category: JavaScript
date: 2014-09-18
math: true
---

MathJax的体积非常大，有60几MB。但可以精简到几MB甚至几百KB。  

我为Jekyll精简了一个MathJax，2.4.0版。分享一下。  
下载：[MathJax For Jekyll](/blog/2014/09/18/Mathjax-2.4.0-For-Jekyll.zip)

默认行内公式用的是`\\(`和`\\)`括起来的，用着不太方便。可以在script这样设置一下：

	MathJax.Hub.Config({
	  tex2jax:{
	    inlineMath: [['\\','\\']],
	    displayMath: [['$$','$$']]
	  }
	});

这样表示行内公式用`\\`括起来，行间公式用`$$`括起来。

<!-- more -->

公式演示：

\\E=mc^2\\

> 参考：  
> [http://docs.mathjax.org/en/latest/misc/faq.html#the-mathjax-font-folder-is-too-big-is-there-any-way-to-compress-it](http://docs.mathjax.org/en/latest/misc/faq.html#the-mathjax-font-folder-is-too-big-is-there-any-way-to-compress-it)  
> [https://github.com/mathjax/MathJax-docs/wiki/Guide%3A-reducing-size-of-a-mathjax-installation](https://github.com/mathjax/MathJax-docs/wiki/Guide%3A-reducing-size-of-a-mathjax-installation)
