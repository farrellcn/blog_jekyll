---
layout: post
title: 在AMD平台的Win7上安装Max OS X 10.9.0
category: Mac
date: 2014-10-13
---

## 基本配置

> #### 硬件
> 1. CPU: AMD FX6300
> 2. 显卡: GTX650
> 3. 8G或以上的U盘 
> 4. MBR引导

> #### 软件
> 1. Windows7系统
> 2. Mac OS X 10.9.0镜像
> 3. win32diskimager、Win版Chameleon、EasyBCD、


## 准备

先下载镜像：[http://pan.baidu.com/s/1mgj0vyS](http://pan.baidu.com/s/1mgj0vyS) 提取密码: h3k3  
[下载win32diskimager]({{ site.blog.qiniu }}/blog/2014/10/13/win32diskimager-v0.9.zip)，打开之。  
然后一如既往地把镜像写入到U盘，详细请步骤自行Google。  
重启，进入BIOS里把U盘设置为第一启动。开启硬盘`AHCI`。

好了，准备就到这里了。

<!-- more -->

## 安装

重启进入U盘引导，光标选中当前的U盘，由于是FX系列的CPU[^1]，故输入`amdfx -v`，就像下图：  
![01]({{ site.blog.qiniu }}/blog/2014/10/13/01.jpg)

之后会进入以下界面  
![02]({{ site.blog.qiniu }}/blog/2014/10/13/02.jpg)

稍等一会，就会进入安装界面  
![03]({{ site.blog.qiniu }}/blog/2014/10/13/03.jpg)

接着找到磁盘工具，进行格式化分区之类的步骤，完了之后回到安装界面，选中一个要安装的分区  
![04]({{ site.blog.qiniu }}/blog/2014/10/13/04.jpg)

点击`自定`，找到以下选项进行以下操作：

{% highlight bash %}
Boot-Loader --> Chameleon --> Chameleon Standard                                                                     [勾选，如果是EFI引导就勾选EFI的选项]
Graphic --> GraphicEnabler                                                                                           [取消勾选]
Boot-Loader Flags --> Chameleon Configuration --> Chameleon Boot Flags --> General Options --> UseKernelCache=YES    [取消勾选]
{% endhighlight %}

![05]({{ site.blog.qiniu }}/blog/2014/10/13/05.jpg)
![06]({{ site.blog.qiniu }}/blog/2014/10/13/06.jpg)

开始安装  
![07]({{ site.blog.qiniu }}/blog/2014/10/13/07.jpg)

安装完会自动重启，又进入引导界面，这次把光标移到到Mac系统所在的磁盘，输入：`UseKernelCache=no`，回车  
![08]({{ site.blog.qiniu }}/blog/2014/10/13/08.jpg)

然后进入Mac系统，进行系统配置  
![09]({{ site.blog.qiniu }}/blog/2014/10/13/09.jpg)
![10]({{ site.blog.qiniu }}/blog/2014/10/13/10.jpg)
![11]({{ site.blog.qiniu }}/blog/2014/10/13/11.jpg)

随后完全进入系统，安装完毕！


## 配置引导

接上一步，重启系统，进入Win7。  
下载：[Chameleon]({{ site.blog.qiniu }}/blog/2014/10/13/Chameleon-Install-2281.zip)、[EasyBCD]({{ site.blog.qiniu }}/blog/2014/10/13/EasyBCD.zip)、[wowpc.iso]({{ site.blog.qiniu }}/blog/2014/10/13/wowpc.iso)

1. 打开Chameleon，进行安装引导。
2. 把下载到的wowpc.iso文件覆盖到C盘根目录。
3. 打开EasyBCD，进行如下配置。

![12]({{ site.blog.qiniu }}/blog/2014/10/13/12.png)

这样，就基本完成了Mac在AMD平台下的安装了，重启选择Mac的引导项就能进入了。

> PS: 用了两天Mac OS，感到水土不服，果断用回Linux，还是Linux大法好！

[^1]: 其他AMD的CPU输入：`amd -v`
