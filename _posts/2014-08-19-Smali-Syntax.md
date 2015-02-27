---
layout: post
title: Smali语法
category: Android开发
date: 2014-08-19
---

> 本文转自：[http://bbs.pediy.com/showthread.php?t=151769](http://bbs.pediy.com/showthread.php?t=151769)

----------

## Dalvik字节码
Dalvik字节码有两种类型，原始类型和引用类型。对象和数组是引用类型，其它都是原始类型。

{% highlight java %}
V void，只能用于返回值类型
Z boolean
B byte
S short
C char
I int
J long (64位)
F float
D double (64位)
{% endhighlight %}

对象以`Lpackage/name/ObjectName;`的形式表示。前面的`L`表示这是一个对象类型，`package/name/`是该对象所在的包，`ObjectName`是对象的名字，`;`表示对象名称的结束。相当于java中的`package.name.ObjectName`，例如：`Ljava/lang/String;`相当于`java.lang.String`。  

<!-- more -->

## 数组的表示形式
`[I`表示一个整型`一维数组`，相当于java中的`int[]`。  
对于多维数组，只要增加`[`就行了。`[[I`相当于`int[][]`，`[[[I`相当于`int[][][]`。注意每一维的最多255个。  
对象数组的表示：`[Ljava/lang/String;`表示一个`String对象数组`。  

## 方法
表示形式：`Lpackage/name/ObjectName;->MethodName(III)Z`  
`Lpackage/name/ObjectName;`表示类型，`MethodName`是方法名。`III`为参数(在此是3个整型参数)，`Z`是返回类型(bool型)。  
方法的参数是一个接一个的，中间没有隔开。  

## 一个更复杂的例子
在Dalvik字节码中为：

{% highlight java %}
method(I[[IILjava/lang/String;[Ljava/lang/Object;)Ljava/lang/String;
{% endhighlight %}

在Java中则为：

{% highlight java %}
String method(int, int[][], int, String, Object[])
{% endhighlight %}

## 字段
表示形式：`Lpackage/name/ObjectName;->FieldName:Ljava/lang/String;`，即包名，字段名和各字段类型。

## 寄存器
在Dalvik字节码中，寄存器都是32位的，能够支持任何类型。64位类型(Long和Double型) 用2个寄存器表示。  
有两种方式指定一个方法中有多少寄存器是可用的。`.registers指令`指定了方法中寄存器的总数。`.locals指令`表明了方法中非参寄存器的数量。

## 方法的传参
当一个方法被调用的时候，方法的参数被置于`最后N个`寄存器中。如果一个方法有2个参数，5个寄存器(v0-v4)，那么参数将置于最后2个寄存器(v3和v4)。  
非静态方法中的第一个参数总是调用该方法的对象。  

例如，非静态方法`LMyObject;->callMe(II)V`有2个整型参数，另外还有一个隐含的`LMyObject;`参数，所以总共有3个参数。假如在该方法中指定了5个寄存器(v0-v4)，以`.registers`方式指定5个或`以.locals方式`指定2个(即2个local寄存器和3个参数寄存器)。当该方法被调用的时候，调用该方法的对象(即this引用)存放在v2中，第一个整型参数存放在v3中，第二个整型参数存放在v4中。  
对于`静态方法`除了`没有隐含的this参数`外其它都一样。

## 寄存器的命名方式
有两种方式：`V命名方式`和`P命名方式`。P命名方式中的第一个寄存器就是方法中的第一个参数寄存器。在下表中我们用这两种命名方式来表示上一个例子中有5个寄存器和3个参数的方法。  

{% highlight java %}
v0 第一个local register
v1 第二个local register
v2 p0 第一个parameter register
v3 p1 第二个parameter register
v4 p2 第三个parameter register
{% endhighlight %}

你可以用任何一种方式来引用参数寄存器，他们没有任何差别。  
注意：baksmali默认对参数寄存器使用P命名方式。如果想使用V命名方式，可以使用`-pl—no-parameter-registers`选项。  
使用P命名方式是为了防止以后如果要在方法中增加寄存器，需要对参数寄存器`重新进行编号`的缺点。  

## Long/Double值
Long和Double类型是64位的，需要2个寄存器(切记)。  
例如：对于非静态方法`LMyObject;->MyMethod(IJZ)V`，参数分别是LMyObject;，int，long，bool。故该方法需要5个寄存器来存储参数。  

{% highlight java %}
p0 this
p1 I
p2,p3 J
p4 Z
{% endhighlight %}

补充：

{% highlight java %}
# static fields      定义静态变量的标记
# instance fields    定义实例变量的标记
# direct methods     定义静态方法的标记
# virtual methods    定义非静态方法的标记
{% endhighlight %}

构造函数的返回类型为V，名字为`<init>`。 

`if-eq p1, v0, :cond_8`表示如果p1和v0相等，则执行`cond_8`的流程

{% highlight java %}
:cond_8
invoke-direct {p0}, Lcom/paul/test/a;->d()V
{% endhighlight %}

调用com.paul.test.a的d()方法  
`if-ne p1, v0, :cond_b`表示`不相等`则执行`cond_b`的流程

{% highlight java %}
:cond_b
const/4 v0, 0×0
invoke-virtual {p0, v0}, Lcom/paul/test/a;->setPressed(Z)V
invoke-super {p0, p1, p2}, Landroid/view/View;->onKeyUp(ILandroid/view/KeyEvent;)Z
move-result v0
{% endhighlight %}
 
大概意思就是调用com.paul.test.a的`setPressed()`方法，然后再调用父类View的`onKeyUp()`方法，最后`return v0`  

## 例子

### 例子1

{% highlight java %}
sget-object v5, Lcom/google/youngandroid/runtime;->Lit227:Lgnu/mapping/SimpleSymbol;
{% endhighlight %}

获取com.google.youngandroid.runtime中的`Lit227字段`存入v5寄存器，相当于

{% highlight java %}
gnu.mapping.SimpleSymbol localVariable = com.google.youngandroid.runtime.Lit227;
{% endhighlight %}

### 例子2

{% highlight java %}
sput-object v0, Lcom/google/youngandroid/runtime;->Lit78:Lkawa/lang/SyntaxTemplate;
{% endhighlight %}

同样，这是设置一个静态字段的值。设置com.google.youngandroid.runtime.Lit78的值为v0寄存器中的`kawa.lang.SyntaxTemplate类型`变量的值，相当于：

{% highlight java %}
com.google.youngandroid.runtime.Lit78 = kawa.lang.SyntaxTemplate localVariable;  
{% endhighlight %}


剩下的比较简单你应该能明白了。  
