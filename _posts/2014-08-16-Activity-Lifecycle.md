---
layout: post
title: Activity生命周期
category: Android开发
date: 2014-08-16
---

在Android的学习和开发的过程中，会经常用到`Activity生命周期`的知识，所以初学者**必须掌握**。  

这是Google官方给出的Activity生命周期流程图：  
![Activity-Lifecycle](/blog/2014/08/16/Activity-Lifecycle.png)  

<!-- more -->

`Activity`继承了`ApplicationContext`这个类，我们可以重写以下方法：
{% highlight java %}
public class Activity extends ApplicationContext {
	protected void onCreate(Bundle savedInstanceState);
	protected void onStart();
	protected void onRestart();
	protected void onResume();
	protected void onPause();
	protected void onStop();
	protected void onDestroy();
}
{% endhighlight %}

## Demo
下面我用例子演示一下：
{% highlight java %}
package com.pexcn.activity.demo;

import android.app.Activity;
import android.os.Bundle;
import android.util.Log;

public class Main extends Activity {
	private static final String TAG = "ActivityDemo";
	
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
        Log.e(TAG, "onCreate() start...");
    }
    
	@Override
	protected void onStart() {
		super.onStart();
		Log.e(TAG, "onStart() start...");
	}
	
	@Override
	protected void onRestart() {
		super.onRestart();
		Log.e(TAG, "onRestart() start...");
	}
	
	@Override
	protected void onResume() {
		super.onResume();
		Log.e(TAG, "onResume() start...");
	}
	
	@Override
	protected void onPause() {
		super.onPause();
		Log.e(TAG, "onPause() start...");
	}
	
	@Override
	protected void onStop() {
		super.onStop();
		Log.e(TAG, "onStop() start...");
	}
	
	@Override
	protected void onDestroy() {
		super.onDestroy();
		Log.e(TAG, "onDestory() start...");
	}
}
{% endhighlight %}

**运行Demo**  
在Logcat会显示：  
![Demo-01](/blog/2014/08/16/Demo-01.png)  
这说明当一个Activity`显示出来`的时候会先后执行：`onCreate() -> onStart() -> onResume()`这三个方法。  

**按下BACK键**  
![Demo-02](/blog/2014/08/16/Demo-02.png)  
一个应用程序被按下`BACK`键的时候会先后执行：`onPause() -> onStop() -> onDestory()`这三个方法。  

**按下HOME键**  
![Demo-03](/blog/2014/08/16/Demo-03.png)  
一个应用程序被按下`HOME`键的时候会先后执行：`onPause() -> onStop()`这两个方法。  

**再次启动应用程序**  
![Demo-04](/blog/2014/08/16/Demo-04.png)  
当我们`再次启动`应用程序的时候会先后执行：`onRestart() -> onStart() -> onResume()`这三个方法。  

Activity的生命周期基本就这样子。  
