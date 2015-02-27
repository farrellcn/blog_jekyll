---
layout: post
title: Jekyll常见问题集
category: Jekyll
date: 2014-09-06
---

> 这是一篇记录Jekyll使用时出现的问题的文章。  
> 暂时记录的只有一个问题。。。

## 没有安装wdm
安装完Jekyll，运行`jekyll serve -w`调试博客的时候，会出现这个警告：

{% highlight bash %}
require 'rbconfig'
gem 'wdm', '~> 0.1.0' if RbConfig::CONFIG['target_os'] =~ /mswin|mingw/i
{% endhighlight %}

Google了一番后，原来是没有安装wdm的问题，运行以下命令解决：

{% highlight bash %}
gem install wdm
{% endhighlight %}

<!-- more -->

![01](/blog/2014/09/06/01.png)