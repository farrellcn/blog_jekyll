---
layout: post
title: Activity详解和Task
category: Android开发
date: 2014-11-10
---

## Activity生命周期

* `onCreate()`: 生命周期第一个被调用的方法，主要用来初始化界面。
* `onStart()`: 当Activity显示在界面时，该方法被调用。
* `onRestart()`: 当Activity从停止状态到活动状态前，该方法被调用。
* `onResume()`: 当Activity能够与用户交互，该方法被调用。此时Activity处于Activity栈的栈顶。
* `onPause()`: 当Activity进入暂停状态时，该方法被调用。一般用于保存持久数据或释放资源。
* `onStop()`: 使Activity进入停止状态。
* `onDestroy()`: Activity被销毁时，该方法被调用。

这七个方法定义了Activity的完整生命周期。

1. 初始化：`onCreate() --> onStart() --> onResume()`
2. 按下返回键：`onPause() --> onStop() --> onDestory()`
3. 按下HOME键：`onPause() --> onStop()`
4. 按下HOME后再次启动：`onRestart() --> onStart() --> onResume()`

* 完整的生命周期：开始于`onCreate()`，结束于`onDestory()`
* 可见的生命周期：开始于`onStart()`，结束于`onStop()`
* 活跃的生命周期：开始于`onResume()`，结束于`onPause()`

<!-- more -->

## Activity状态

有四种状态

1. 活动：Activity位于栈顶，可见，有焦点，可交互。
2. 暂停：没有焦点，不可交互，但是任然属于活动状态。
3. 停止：不可见，但仍然在内存中保存程序状态。
4. 待用：被移除Activity栈，当需要时重新启动它。

## 两个非生命周期的方法

**onRestoreInstanceState(Bundle savedInstanceState)**  
onCreate()完成后被调用，用于恢复UI状态

**onSaveInstanceState(Bundle savedInstanceState)**  
即将被移除Activity栈顶时被调用(程序发生意外情况)，用来保存UI状态

----------

## StartActivityForResult

用于从第二个Activity把数据返回到第一个Activity

用法：

1. 在第一个Activity重写`onActivityResult()`方法 ---> 数据返回之后与来干什么
2. 调用第二个Activity时使用`startActivityForResult()`方法 ---> 进入第二个Activity
3. 被调用Activity在`finish()`之前调用`setResult()` ---> 返回数据到第一个Activity

----------

## Task和Affinity

简单的讲，一个Task就是用户体验上的“应用程序”，就是一组Activity的集合。而Affinity就是表示Activity的亲和度，表明了该Activity属于哪个Task。默认情况下，一个应用程序的所有Activity都有相同的Affinity。

**taskAffinity属性**  
表示该Activity属于哪个Task，默认值是该应用程序的包名。例如：一个Activity_A跳转到Activity_B中，两者的taskAffinity属性相同，则它们在同一个Task中，如果不同，那么跳转到Activity_B的时候会创建一个新的Task。

**allowTaskReparenting属性**  
标记Activity能否更换所从属的Task到taskAffinity指定的Task中。默认值是false，表示不可更换，true则表示可以更换。

**FLAG_ACTIVITY_NEW_TASK标记**  
如果已经存在一个Task与新Activity的Affinity一样，该Activity将启动到该Task。如果不是，则启动一个新Task。

----------

## Activity启动模式

**standard**  
默认模式，每次都创建Activity的新实例。

**singleTop**  
与standard模式类似，但是如果要启动的Activity新实例刚好位于Activity栈的栈顶(可见状态)，则会重用之，不会建立新Activity的实例。

**singleTask**  
栈中只能有这样一个Activity实例。如果栈中已经有该Activity的实例，则会重用改实例。重用时，会把它移动到栈顶。不存在则会建立它的实例。

**singleInstance**  
这种模式的Activity单独存在于一个栈中，并让多个应用程序重用它。

----------

## 清除栈

当用户离开一个应用程序很久，系统会自动清理除了根Activity之外的Activity。

**alwaysRetainTaskState属性**  
如果根Activity的这个属性设置为true，则以上情况不会发生，系统不会自动清理Activity。

**clearTaskOnLaunch属性**  
如果根Activity的这个属性设置为true，情况则与alwaysRetainTaskState属性恰恰相反。当用户离开之后，系统会立刻清除Activity，所以离开后用户再次进入都会显示程序的初始状态。

**finishOnTaskLaunch属性**  
这个属性类似于clearTaskOnLaunch，但是它作用于单个活动，而不是整个Task。它能清除本程序的任何Activity，包括根Activity。
