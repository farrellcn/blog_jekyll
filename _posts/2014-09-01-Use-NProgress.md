---
layout: post
title: 简单使用NProgress
category: JavaScript
date: 2014-09-01
---

虽然还没有学JavaScript，但是有之前的学习C语言、Java的基础，看着参考文档使用这些Js开源库应该不是很大问题，下面来介绍一下`NProgress`的使用，顺便做个记录。

NProgress应该是一个进度条控件之类的吧，具体作用就是在网页上显示进度。

## 使用

首先要在HTML里加入这两行，把css和js载入进来

{% highlight html %}
<link rel="stylesheet" href="nprogress.css">
<script type="text/javascript" src="nprogress.js"></script>
{% endhighlight %}

	NProgress.start();		// 进度条开始
	NProgress.set(0.5);		// 进度设置为0.5
	NProgress.inc();		// 进度增加一点
	NProgress.done();		// 完成进度条

## 演示

<p>
  <button onclick="NProgress.start();">进度条开始</button>
  <br/>
  <button onclick="NProgress.set(0.5);">进度设置为0.5</button>
  <br/>
  <button onclick="NProgress.inc();">进度增加一点</button>
  <br/>
  <button onclick="NProgress.done();">完成进度条</button>
</p>

## 分享

分享一个修改了高度的NProgress：[下载](/blog/2014/09/01/nprogress-0.1.6.zip)

> NProgress项目主页：[https://github.com/rstacruz/nprogress/](https://github.com/rstacruz/nprogress/)
