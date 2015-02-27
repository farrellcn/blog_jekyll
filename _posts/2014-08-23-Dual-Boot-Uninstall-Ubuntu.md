---
layout: post
title: Windows和Ubuntu双系统卸载Ubuntu
category: Linux
date: 2014-08-23
---

> 这篇博文是从旧的博客搬上来的。  
> 仅仅只是做个记录而已，写的有点简短。

1. 首先，进入Windows，下载[MBRFix.exe](/blog/2014/08/23/MBRFix.exe)

2. 定位到`MBRFix.exe`所在的目录，运行：`MBRFix.exe /drive 0 fixmbr`

3. 再按`Y`，确认一下。

4. 再进入Windows的磁盘管理，把Ubuntu所在的分区删掉，重启系统，Ubuntu就卸载完成了。  
