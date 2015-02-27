---
layout: post
title: 同步Android源码的技巧
category: Android开发
date: 2014-08-19
---

## 软链接
首先你得完全同步一次源码，比如是CyanogenMod 10.1的源码，目录在`~/cm10.1`  
那么在第二次同步源码，比如同步CyanogenMod 10.2的源码，就可以用到软链接了，设定目录在`~/cm10.2`。  
需要链接的文件为：`projects`和`project.list`  

命令：`ln -s <目标文件/目录> <软链接文件/目录>`

命令示例：
{% highlight bash %}
ln -s ~/cm10.1/.repo/projects ~/cm10.2/.repo/projects
ln -s ~/cm10.1/.repo/project.list ~/cm10.2/.repo/project.list
{% endhighlight %}

## 深度搜索
`git`或`repo`都提供了`深度搜索`这个功能，它可以只下载最近`n`次的历史。  

命令选项：`--depth=n`，`n`表示最近`n`次历史。  

命令示例：
{% highlight bash %}
# 表示只下载最近1次历史，这样下载源码的速度大大加快了
repo init -u git://github.com/CyanogenMod/android.git -b cm-11.0 --depth=1
{% endhighlight %}
