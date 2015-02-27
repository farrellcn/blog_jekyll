---
layout: post
title: Archlinux安装小记
category: Linux
date: 2014-10-16
---

两块硬盘，打算一块用来装Windows，一块用来装Archlinux。

### 建立分区

`用cfdisk`命令来建立分区，由于是第二块硬盘，所以：`cfdisk /dev/sdb`，然后按需求设置分区。

### 格式化分区

下面是我的命令，仅供参考：
{% highlight bash %}
mkfs.ext4 /dev/sdb1    # 根目录
mkfs.ext4 /dev/sdb5    # 普通ext4分区
mkswap /dev/sdb6       # 建立swap
swapon /dev/sdb6       # 启用swap
{% endhighlight %}

<!-- more -->

### 更换更快的源
{% highlight bash %}
echo > /etc/pacman.d/mirrorlist
nano /etc/pacman.d/mirrorlist
{% endhighlight %}

在里面输入速度较快的源，如：
{% highlight bash %}
Server=http://mirrors.163.com/archlinux/$repo/os/$arch
Server=http://mirrors.bjtu.edu.cn/archlinux/$repo/os/$arch
{% endhighlight %}

### 设置WiFi

由于我的所无线网卡，所以命令行`wifi-menu`来设置WiFi。

### 挂载分区
{% highlight bash %}
mount /dev/sdb1 /mnt
{% endhighlight %}

### 安装基本系统
{% highlight bash %}
pacstrap /mnt base
{% endhighlight %}


### 配置系统
{% highlight bash %}
# 生成fstab
genfstab -p /mnt >> /mnt/etc/fstab

# changeroot到新系统
arch-chroot /mnt

# 设置主机名
echo <主机名> > /etc/hostname

# 设置时区
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

# 创建初始Ramdisk
mkinitcpio -p linux

# 设置root密码
passwd root

# 装网卡驱动
pacman -S dialog wpa_supplicant

# 退出chroot
exit

# 卸载分区
umount -R /mnt

# 重启电脑
reboot

{% endhighlight %}

### 配置引导
用EasyBCD，`NeoGrub`引导，写入：
{% highlight bash %}
root (hd1,0)                                # 参数：(hd第几块硬盘，第几分区)
kernel /boot/vmlinuz-linux root=/dev/sdb1   # 参数：路径可用ext4explorer查看，root=/dev/sdx分区号
initrd /boot/initramfs-linux.img            # 参数：initrd路径
boot
{% endhighlight %}

系统就装好了，不过还差那坑爹的`X Window`...[^1]

[^1]: 好几次装桌面环境把整个系统搞挂掉了。不折腾了。。。

