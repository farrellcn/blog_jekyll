---
layout: post
title: Discuz论坛的备份与还原
category: 云平台
date: 2014-08-28
---

> 简单记录下，避免下次再出问题。  
> 环境是在BAE搭建的。  

## 备份
先把数据库备份了，用phpMyAdmin也好什么都好，下次能正确还原就行。  

据说还要把以下这几个目录备份了，虽然我没测试。。。

> 会员头像目录：`uc_server/data/avatar`和`tmp`目录  
> 各应用附件和图片目录：`data/attachment`目录  
> 插件目录：`source/plugin`目录 (官方默认那几个不要)  
> 模板文件：`template/目录下的几个对应模板`  

## 还原
把数据库备份好的`.sql`文件还原。  

把`config目录`下的几个`.php`文件(应该只需要改两个，虽然我全改了。。。)的配置改为你现在数据库的配置。  
还要把`uc_server/data/config.inc.php`文件也改为你现在数据库的配置。  

<!-- more -->

需要修改的大概就有以下关键字的几个值

{% highlight bash %}
DBHOST
DBUSER
DBPW
DBNAME
{% endhighlight %}

另外，`config_ucenter.php`文件还需要修改`UC_DBTABLEPRE`这个参数，把它后面的`root`值改为你的数据库名。  

整个备份与还原的过程就大概这样子了。  
