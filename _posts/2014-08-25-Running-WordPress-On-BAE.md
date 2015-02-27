---
layout: post
title: 在BAE上搭建WordPress博客
category: 云平台
date: 2014-08-25
---

App Engine是个好东西，很早就听说有什么[BAE](http://developer.baidu.com/)、[SAE](http://sae.sina.com.cn/)、[GAE](http://appengine.google.com/)...  
之前一直不知道这东西是什么，今天才知道这东西是个云平台、网络应用引擎之类的东西。  
今天有空就试了试在BAE上搭建[WordPress](http://cn.wordpress.org/)博客，顺便做个记录。

## 准备
> 1. 开始之前要在[BAE](http://developer.baidu.com/)上注册个百度开发者账号。  
> 2. [git](http://www.git-scm.com/)代码管理工具

## 创建应用引擎和数据库
在[百度应用引擎](http://developer.baidu.com/cloud/rt)里创建一个工程。  

> 类型选：php-web  
> 因为我不会svn，所以代码管理工具我选：git  

再创建一个数据库，如图，在`应用引擎 --> 扩展服务 --> 添加新服务`里选择MySQL  

<!-- more -->

## 移植WordPress
先在[WordPress官网](http://cn.wordpress.org/)下载安装包，我下载的是3.9版的。  
再把安装文件解压到本地，找到`wp-config-sample.php`或`wp-config.php`，打开之。  

找到`DB_NAME`，把它后面的值改为`数据库的名称`  
找到`DB_USER`，把它后面的值改为`API Key`  
找到`DB_PASSWORD`，把它后面的值改为`Secret Key`  
找到`DB_HOST`，把它后面的值改为`数据库的连接地址和端口`，如：`sqld.duapp.com:4050`  

## 推送安装文件
先要在git里把你项目的仓库clone下来

{% highlight bash %}
git clone 仓库地址
{% endhighlight %}

再把仓库初始化

{% highlight bash %}
git init
{% endhighlight %}

把原来的origin删除
{% highlight bash %}
git remote rm origin
{% endhighlight %}

再把你的origin添加进去
{% highlight bash %}
git remote add origin 仓库地址
{% endhighlight %}

把修改后的安装文件复制进来，再正常push上去
{% highlight bash %}
git add .
git commit -m "init"
git push origin master
# User填你的百度账号
# Password填你的百度账号的密码
{% endhighlight %}

这时候会出错，因为要推送的文件大小受到git的限制了，执行以下命令得以解决
{% highlight bash %}
git config http.postBuffer 524288000
{% endhighlight %}

之后重新push即可。

## 安装WordPress
点击`BAE --> 项目主面板 --> 应用引擎 --> 操作 --> 快捷发布`
在浏览器打开你项目的首页，然后会提示安装，安装过程非常简单，不再赘述。  

## WordPress
到这里，WordPress就安装完成了，虽然我不用。。。  

![WordPress](/blog/2014/08/25/wordpress.png)  

> **参考**  
> [http://developer.baidu.com/wiki/index.php?title=docs/cplat/bae/wordpress](http://developer.baidu.com/wiki/index.php?title=docs/cplat/bae/wordpress)  
