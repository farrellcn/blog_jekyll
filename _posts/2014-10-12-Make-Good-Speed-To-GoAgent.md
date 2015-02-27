---
layout: post
title: 为GoAgent翻墙加速
category: 翻墙
date: 2014-10-12
---

## 添加多个appid

在GoAgent的`proxy.ini`配置文件里，有一行以`appid = `开头的代码，只要在它后面添加多个在GAE部署的app，就可以达到加速的目的。  
appid之间用`|`分隔。例如：
{% highlight ini %}
appid = appid01|appid02|appid03|appid04|appid05
{% endhighlight %}

## 开启pagespeed选项

同样的，在`proxy.ini`这个配置文件里，有一个`pagespeed`选项，数值为0，表示默认关闭。把它改成1，表示开启。  
同时必须要把`obfuscate`选项打开，它的值也改为1。  
例如：

{% highlight ini %}
obfuscate = 1
pagespeed = 1
{% endhighlight %}

<!-- more -->

## 更新iplist

先下载`Gogo Tester`工具：[点击下载](/blog/2014/10/12/Gogo-Tester-v2.3.4.zip)  
打开它，然后`开始随机测试`

![01](/blog/2014/10/12/01.png)

把测试出来的ip地址复制到`proxy.ini`的如下位置：

{% highlight ini %}
[iplist]
google_cn = #把IP复制到这里来
google_hk = #把IP复制到这里来
{% endhighlight %}

之后再次启动GoAgent就会看到效果了。  
如图所示：`good_ipaddrs`表示ip可用，`bad_ipaddrs`表示ip不可用。

![01](/blog/2014/10/12/02.png)

#### 2014-10-20更新：
> 我还发现了一个叫gscan的工具，类似于Gogo Tester，它的速度更快，更准确。  
> [下载gscan.zip](/blog/2014/10/12/gscan.zip)  

## 关闭https开启RC4加密

在GoAgent的目录里找到`server/gae/gae.py`这个文件，打开，把里面`__password__`的值改为你要改的密码。  
然后在`proxy.ini`里面，找到gae的配置项并修改配置。例如：

{% highlight ini %}
appid = APPID           # 你的appid
password = PASSWORD     # 改成你在`gae.py`修改的密码
......
mode = http             # 改成http
......
options = rc4           # 改成RC4
{% endhighlight %}
