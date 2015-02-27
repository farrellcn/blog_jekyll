---
layout: post
title: 安装完Mac OS后的系统配置
category: Mac
date: 2014-10-15
---

用了两天Mac OS，感到水土不服，果断用回Linux。

下面是安装完Mac OS之后的系统配置，再此备份一下，避免可能有下次安装Mac OS......

## 一些配置

#### 更改管理员密码
{% highlight bash %}
sudo passwd root
{% endhighlight %}

#### 安装brew
{% highlight bash %}
sudo su
curl -L http://github.com/mxcl/homebrew/tarball/master | tar xz --strip 1 -C /usr/local
{% endhighlight %}

<!-- more -->

#### 终端彩色化
用户主目录新建`.bash_profile`文件，输入：
{% highlight bash %}
export CLICOLOR=1
export PS1='\[\033[01;33m\]\u@\h\[\033[01;31m\] \w\$\[\033[00m\] '
alias grep='grep --color=always'
{% endhighlight %}

#### Finder显示隐藏文件
{% highlight bash %}
defaults write com.apple.finder AppleShowAllFiles -bool true
{% endhighlight %}
隐藏就改为`false`
{% highlight bash %}
killall Finder
{% endhighlight %}

---------

## 必装软件

> Chrome  
> Hoststool  
> iYY  
> QQ  
> ShadowsocksX  
> GoAgentX  
> 搜狗输入法  
> 迅雷  
>
> ADT  
> git  
> Intellij IDEA  
> JDK  
>
> Chameleon  
> Chameleon Wizard  
> iStatMenus  
> iTerm2  
> Karabiner  
> LocalTimeToggle  
> The Unarchiver  
> TinkerTool  
> XtraFinder  
> VoodooHDA  
