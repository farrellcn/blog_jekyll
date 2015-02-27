---
layout: post
title: 在Ubuntu上搭建Jekyll环境
category: Linux
date: 2014-10-18
---

环境所Ubuntu12.04，输入几条命令就可以在搭建Jekyll的环境来，简单的很啊。

命令如下：
{% highlight bash %}
# 安装Ruby
sudo apt-get install ruby1.9.3

# 用gem安装一些Jekyll的库
sudo gem install jekyll
sudo gem install therubyracer
sudo gem install rouge
sudo gem install rdiscount
sudo gem install rake
{% endhighlight %}
