---
layout: post
title: 给Jekyll的博客安装Fancybox插件
category: Jekyll
date: 2014-08-09
---

`Fancybox`是一个基于`jQuery`开发的类Lightbox插件。可以用来看图、添加阴影效果什么的。。。  
下面来介绍Fancybox的安装在Jekyll的方法。

## 下载Fancybox
这个可以到Fancybox的[**项目主页**](https://github.com/fancyapps/fancyBox/releases)里下载。  
但是我只是用来看图，官方给出的压缩包有很多用不到的东西，所以我也提供一个精简版的：[**本地下载**](/blog/2014/08/09/fancybox-v2.1.5-lite.zip)  

## 使用Fancybox
把下载下来的安装包解压到一个非中文的目录，比如我的是解压到：`/res/js/fancybox`。  
然后在所需要使用Fancybox的页面上插入以下代码：

<!-- more -->

{% highlight html %}
<!-- Fancybox -->
<link rel="stylesheet" href="/res/js/fancybox/jquery.fancybox.css">
<script type="text/javascript" src="/res/js/fancybox/jquery-1.11.0.min.js"></script>
<script type="text/javascript" src="/res/js/fancybox/jquery.fancybox.pack.js"></script>
<script>
	$('.post-main').each(function (i) {
        $(this).find('img').each(function () {
            var url = this.src;
            $(this).wrap('<a href="' + url + '" class="fancybox"></a>');
        });
        $(this).find('.fancybox').each(function () {
            $(this).attr('rel', i);
        });
    });
    $('.fancybox').fancybox({
		padding:7,
		openEffect:'fade',
		closeEffect:'fade',
		scrolling:'no',
    });
</script>
{% endhighlight %}

不过要把引用的路径改为你自己的。下面`$("#img").fancybox`开头那段是配置Fancybox特效之类的。。可以在[**官网**](http://fancybox.net/)查看详细说明。  
