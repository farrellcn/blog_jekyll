---
layout: post
title: 设置ccache编译Android源码
category: Android开发
date: 2014-08-19
---

## 环境
> 系统：Ubuntu 12.04  
> ccache路径：~/Android/Source/ccache

## 设置
添加环境变量，开启ccache

{% highlight bash %}
export USE_CCACHE=1
{% endhighlight %}

建立缓存目录

{% highlight bash %}
export CCACHE_DIR=~/Android/Source/ccache    #目录可以改变，这里以我的ccache路径为例
{% endhighlight %}

设置缓存大小，定位到源码目录，执行

{% highlight bash %}
prebuilt/linux-x86/ccache/ccache -M 20G      #设置20GB为例
或者
prebuilts/misc/linux-x86/ccache/ccache -M 20G
{% endhighlight %}

<!-- more -->

查看ccache使用率

{% highlight bash %}
watch -n1 -d prebuilt/linux-x86/ccache/ccache -s
或者
watch -n1 -d prebuilts/misc/linux-x86/ccache/ccache -s
{% endhighlight %}
