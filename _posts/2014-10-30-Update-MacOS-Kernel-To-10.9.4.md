---
layout: post
title: 在AMD平台下升级OSX的内核到10.9.4
category: Mac
date: 2014-10-30
---

原帖地址：[http://www.hackintoshosx.com/files/file/4210-amd-kernel-for-os-x-mavericks-1094-xnu1330/](http://www.hackintoshosx.com/files/file/4210-amd-kernel-for-os-x-mavericks-1094-xnu1330/)

我的CPU是FX6300，看到内核有更新了，果断更新。把原帖里的内核下载下来，或者[点击这里]({{ site.blog.qiniu }}/blog/2014/10/30/OSX10.9.4-Kernel-For-AMD.zip)下载。

### 更新过程

1. 把压缩包的`deekay_kernel`改为`mach_kernel`，解压到根目录。
2. 驱动解压到`S/L/E`
3. 重启，如果重启不成功，则试试用U盘引导进入终端执行以下命令修复权限。

{% highlight bash %}
cd V*
cd Mac系统盘名称
chown root:wheel mach_kernel
chown -R root:wheel /System/Library/Extensions/
{% endhighlight %}
