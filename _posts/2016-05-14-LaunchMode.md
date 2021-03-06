---
layout: post
title:  "Activity的启动模式"
categories: 
 - 博客
date:   2016-05-14 12:15:13
nocomments: false
---


# Activity的启动模式

**导语：**

_Activity的启动模式是初学者最头疼的地方了，形形色色的启动模式和标志位实在是太容易被混淆了，但是Activity作为四大组件之首，它的的确确非常重要，有时候为了满足项目的需求，就必须使用Activity的启动模式，所以我们要搞清楚它的启动模式和标志位。_

###Activity的LauncherMode
首先说一下Activity为什么需要启动模式。我们知道，在默认情况下，当我们多次启动同一个Activity的时候，系统会创建多个实例并且把它们放到任务栈中，当我们单击back时，会发现这些Activity会一一回退。任务栈是一种“后进先出”的栈结构，当栈中无任何Activity时，系统就会回收这个任务栈。如果按照Activity的默认启动模式，那么就会存在这样一个问题：多次启动同一个Activity系统会多次创建多个重复的实例。所以android提供了四种启动模式来修改系统的默认行为。四种启动模式分别是：standard、singleTop、singleTask、singleInstance。

* **standard:标准模式** 这是系统默认的模式。每次启动一个Activity就会重复创建一个新的实例，不管这个实例是否已经存在。被创建的实例的生命周期符合典型情况下的Activity的生命周期，他们的onCreate、onStart、onResume都会被调用。这是一种典型的多实例实现，一个任务栈中可以有多个实例，每个实例也可以属于不同的任务栈。在这种情况下，谁启动了这个Activity，那么这个Activity就运行在启动它的那个Activity所在的栈中。比如Activity A 启动了Activity B（B是标准模式），那么B就会进入A所在的栈。可能会有人知道，当我们用ApplicationContext 去启动standard模式的Activity的时候会报错：这是因为standard模式的Activity默认会进入启动它的Activity任务栈中，但是由于非Activity类型的Context（如ApplicationContext）没有所谓的任务栈，所以就会报错了。解决这个问题的方法就是为待启动Activity指定FLAG_ACTIVITY_NEW_TASK标记位，这样启动的时候就为他创建了一个新的任务栈，这个时候启动的Activity实际是以singleTask模式启动的。
  
* singleTop
* singleTask
* singleInstance