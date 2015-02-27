---
layout: post
title: 在Windows上运行Jekyll
category: Jekyll
date: 2014-08-08
---

我虽然安装了Ubuntu，但还是觉得Windows用起来顺手一点。下面的在Windows安装Jekyll的教程。  

## 下载和安装Ruby和DevKit
先从[Ruby官网](http://rubyinstaller.org/downloads/)下载2.0.0版本的Ruby安装包 (1.9.3版的也可以)，32位的就下载32位的安装包，64位就下载64位的安装包。我装的是[64位](http://dl.bintray.com/oneclick/rubyinstaller/rubyinstaller-2.0.0-p481.exe)的。  
还有`DevKit`也从[这里](http://rubyinstaller.org/downloads/)下载。  
再把这两个安装包给安装了，路径可以自定义。  

安装完之后把Ruby安装目录下的`bin文件夹`添加到系统的环境变量里。  
再定位到DevKit的目录执行`ruby dk.rb init`，这样会生成一个叫`config.yml`的配置文件。  
在`config.yml`里面添加Ruby的安装路径。  
到这里，就安装好了，下一步就是要安装Jekyll了。

## 下载和安装Python
到[Python官网](https://www.python.org/downloads/)下载2.7版的Python，我装的是2.7.8版的。  

安装Python，安装完后把Python的安装路径添加到环境变量。

<!-- more -->

## 安装Jekyll
在Devkit的目录下，打开命令行输入：`ruby dk.rb install`  
执行完之后，再输入：`gem install jekyll`  
这样静静等待安装结束。。。速度可能很慢，原因大家懂的。。。或许挂VPN或GoAgent速度会好一些。

## 安装Pygments
`Pygments`是语法高亮的插件。  
先到[这里](https://bootstrap.pypa.io/ez_setup.py)下载`ez_setup.py`脚本。  
下载不了的话我提供一个[**备份**](/blog/2014/08/08/ez_setup.py)。  

打开命令行，定位到`ez_setup.py`所在的目录，运行：`python ez_setup.py`。  
然后定位到Python安装目录下的Script目录，运行：`easy_install Pygments`。等待运行结束。。。  
环境的搭建就这样坑爹地结束了。。。

## 运行Jekyll建立博客
命令行输入：`jekyll new blog`，这样建立一个博客  
再`cd blog`定位到博客的目录  
运行`jekyll serve`可以在本地测试了，测试地址是：[*http://127.0.0.1:4000/*](http://127.0.0.1:4000/)  

> 端口可以更改，只要在`_config.yml`添加`port`参数，后面跟端口的值，比如：`port: 3000`

`jekyll serve`有个常用参数：`-w`或`--watch`。  
只要执行`jekyll serve -w`就可以在你修改博客某一文件后立刻生成预览而不用重新执行`jekyll serve`。  

> 另外，安装过程也可以参考：[http://jekyll-windows.juthilo.com/](http://jekyll-windows.juthilo.com/)

![Jekyll](/blog/2014/08/08/2014-08-08-01.png)  
