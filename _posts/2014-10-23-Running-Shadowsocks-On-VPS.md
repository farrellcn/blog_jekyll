---
layout: post
title: 在VPS搭建Shadowsocks
category: 翻墙
date: 2014-10-23
---

今天在[VPS.ME](http://www.vps.me)申请到了免费VPS，我为此兴奋不已。虽然内存只有384MB，但是用来搭建Shadowsocks还是足够的。  
我的VPS的系统是32位的Debian7，只要登陆VPS并执行以下命令，就能搭建Shadowsocks了。

{% highlight bash %}
# 安装依赖
apt-get update
apt-get install build-essential autoconf libtool libssl-dev gcc git nano -y

# 下载shadowsocks-libev源码
git clone https://github.com/madeye/shadowsocks-libev.git
cd shadowsocks-libev

# 编译
./configure
make && make install

# 编辑配置文件
nano ~/shadowsocks/ss.json
# 输入
{
    "server": "::",
    "server_port": 端口,
    "local_port": 本地端口,
    "password": "密码",
    "timeout": 600,
    "method": "加密方法"
}

# 后台运行
nohup ss-server -c ~/shadowsocks/ss.json &
{% endhighlight %}

<!-- more -->

之后只要在你的浏览器配置一下就可以翻墙了。
