---
layout: post
title: 在Heroku上搭建Shadowsocks
category: 翻墙
date: 2014-10-25
---

在逛Github的时候居然发现有Heroku的专用版本的Shadowsocks，果断搭建之。。。

### 准备

* Heroku账号
* 安装Ruby 1.9.3版本
* 安装Node-js任意版本
* 安装git任意版本
* 在Heroku上添加ssh密钥

### 搭建Shadowsocks

前提是把准备的工具都安装好了。  
打开命令行，输入以下命令：

<!-- more -->

{% highlight html %}
# 输入账号密码登陆
heroku login

# 创建应用，如：heroku create appname
heroku create 应用名称

# 下载Shadowsocks的Heroku专版，准备应用程序
git clone https://github.com/mrluanma/shadowsocks-heroku.git
cd shadowsocks-heroku
git init
git commit -m "init"

# 添加remote
heroku git:remote -a 应用名称

# 推送上去
git push heroku master

# 设置加密方法和密码，如：heroku config:set METHOD=rc4 KEY=PASSWORD
# 加密方法推荐rc4和aes-256-cfb
heroku config:set METHOD=加密方法 KEY=密码

# 运行，如：node local.js -s appname.herokuapp.com -l 1080 -m rc4 -k PASSWORD
node local.js -s 应用名称.herokuapp.com -l 本地端口 -m 加密方法 -k 密码
{% endhighlight %}

这样就可以通过设置Firefox或Chrome浏览器的插件翻墙了，速度还可以。

> 参考：[https://github.com/mrluanma/shadowsocks-heroku](https://github.com/mrluanma/shadowsocks-heroku)
