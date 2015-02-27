---
layout: post
title: 更改Mac OS开机动画的分辨率
category: Mac
date: 2014-10-31
---

1. 打开`Extra`目录的`org.chameleon.Boot.plist`

2. 在适当的位置加上以下代码，重启就行了。

{% highlight xml %}
<key>Graphics Mode</key>
<string>显示器的分辨率x32</string>
{% endhighlight %}

简短的教程完毕！[^1]

<!-- more -->

[^1]: 其实只是做个记录备用
