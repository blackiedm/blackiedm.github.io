---
layout: post
title:  "内存泄漏－实践篇"
date:   2016-02-18 11:29:25
categories: android
---

知识点
---

* shallow heap:对象自身内存大小
* retained heap:对象自身及对象所有引用的内存之和,即gc时,回收该对象后一共释放的内存
* gcRoot:垃圾回收器对象
* strong reference:强引用,即使是内存不够时,垃圾回收器不会回收该对象
* soft reference:软引用, 在内存足够时垃圾回收器不会回收该对象,当内存不够时会回收该对象
* weak reference:弱引用,当不再引用时,立即回收    
* ThreadLocal:通过为每个线程提供独立的变量副本解决变量并发访问的问题
* 线程同步机制:通过对象的锁机制保证同一时间只有一个线程访问变量
* Memory Monitor:用于观察整个应用内存变化
* MAT:堆内存分析工具
* Dominator tree: 列出内存中所有对象,及他们所占用的内存大小

步骤
---

* 发现泄露现象
* 定位问题
* 解决问题

### 具体

**发现泄露现象**:通过`Android studio` 的`Memory Monitor` 观察应用内存变化.

**具体操作**:启动应用(此时占用内存达100M左右),退出应用, 同时使用GC操作(此时占用内存没有明显变化,猜想这里发生内存泄露),再次启动应用(此时占用内存从100M升到160M,再次证实应用存在内存泄露)

**定位问题**:启动应用并退出应用,此时应用还在运行,获取内存快照`Dump java heap`,此时生成hprof文件(位置在AS左侧栏`Captures->Heap Snapshot`下),右键生成标准的hprof文件,使用MAT打开,然后打开`dominator tree`,如下

![figure 0](/assets/article_images/2016-02-18-memory_leak/memory_leak_1.png)

有上面截图可知,`PercentRelativeLayout`的`retained Heap`的百分百超过50%,猜想内存泄露可能是它.
这时找到它到gcRoot的路径:右键点击`Path To Gc Roots -> 除了软引用和弱引用`,截图如下

![figure 1](/assets/article_images/2016-02-18-memory_leak/memory_leak_2.png)

角标左下有个小黄点的就是`gcRoot`,此时可初步判断是`InputMethodManager`的调用和`View3Pagers`下的线程池`excutor`的线程出了问题.
当然MAT此外还提供了`Leak Supspects`直接帮你分析出内存泄露的对象,如下

![figure 2](/assets/article_images/2016-02-18-memory_leak/memory_leak_3.png)

第一个问题也是`PercentRelativeLayout`所占内存最多(证明第一次猜想),点击详情查看,

![figure 3](/assets/article_images/2016-02-18-memory_leak/memory_leak_4.png)

MAT直接帮你定位到引起内需泄露的对象`InputMethodManager`

知道了问题所在,那就赶紧解决它吧.
