---
layout: post
title: QQ空间尾巴修改器
category: Android应用
date: 2014-08-12
---

## 这是一个真实故事
作为一个极(zuo)客(si)型小白，写出来的小应用从来只自己用。但是今天群里的大神非要让我共享，结果到底是毁了多少系统。。。？  
本来我自己测试是没有问题的，但是经过群里的大神的一番检测，终于都发现了bug，而且个个机子都挂掉了：应该是误删了作为中继的`sdcard`里的`build.prop`吧？  

## 原理
修改`build.prop`的`ro.product.model`和`ro.product.manufacturer`，`MODEL`是指机型(后半部分)，`MANUFACTURER`是指厂商(前半部分)。  
所以只修改`MANUFACTURER`部分就行了，`MODEL`部分用全角空格代替，如果用半角空格的话会被忽略。  

## 截图
![01](/blog/2014/08/12/2014-08-12-01.png)
![02](/blog/2014/08/12/2014-08-12-02.png)

<!-- more -->

## 下载
[**本地下载**](/blog/2014/08/12/QzoneTailModifier-v1.0.3.apk)

## 使用
> 1. 系统要获取ROOT权限  
> 2. 打开程序，ROOT授权，把尾巴改成你想要的  
> 3. 重启手机  
> 4. 打开QQ ---> 好友动态 ---> 点击尾巴
> 5. 重新选择你刚刚改的尾巴  
> 6. 再发说说或者传图片什么的就能看见你改的尾巴了

**但是我不得不提醒你一句：慎用，因为有人测试过，重启后手机会开不了机。虽然我测试了十几遍。**

## 源码
源码放到GitHub，自己要怎么改怎么改吧  
**GitHub**: [**QzoneTailModifier**](https://github.com/pexcn/QzoneTailModifier)

## 交流群
Android交流群：**61620990**  
欢迎各路大神以及各种伸手党及下限帝前来挑战！  
