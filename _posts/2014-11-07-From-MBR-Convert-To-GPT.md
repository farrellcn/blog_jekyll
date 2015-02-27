---
layout: post
title: 硬盘从MBR格式转换到GPT格式
category: Windows
date: 2014-11-07
---

前几天突然心血来潮想装个Windows8.1，果断装下玩玩。但是遇到个问题，硬盘不可以为MBR格式，果断转换之，但是这样会清空硬盘的数据。[^1]

只需要执行以下步骤：

1. 安装界面下按下键盘的`Shift+F10`打开命令行。

2. 执行以下命令：

<!-- more -->

{% highlight bash %}
# 打开diskport工具
diskport

# 显示所有的硬盘
list disk

# 选择要转换的硬盘，disk 0表示第一块硬盘，以此类推
select disk 0

# 清空它
clean

# 转换成GPT
convert gpt

# 建立两个分区，分别为EFI分区和系统保留分区
create partition efi size=500    # 单位：MB，不能超过512MB
create partition efi size=500    # 同上

# 建立系统安装的盘
create partition primary size=100000

# 查看分区列表
list partition
{% endhighlight %}

之后退出命令行就可以安装系统了。

[^1]: 没什么数据，就把它给转换了。