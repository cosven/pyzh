---
layout: post
title:  Why you can have millions of Goroutines but only thousands of Java Threads
date:   2018-10-10 09:41:42 +0800
categories: goroutine asyncio OS
---

**原文链接**：<https://rcoh.me/posts/why-you-can-have-a-million-go-routines-but-only-1000-java-threads/>

**一句话概括**：从操作系统原理层面介绍为啥 Goroutine 的数量可以比 Java threads 多很多

**摘要**

> In the JVM: Fixed Stack Size -> Using operating system threads incurs a constant, large, memory cost per thread
> Goroutines: How Go does it differently: Dynamically Sized Stacks

> In the JVM: Context Switching Delay -> Using operating system threads caps you in the double digit thousands, simply from context switching delay.
> Goroutines: Run multiple Goroutines on a single OS thread

> Go facilitates this by integrating channels and the scheduler.
> If a goroutine is waiting on a empty channel, the scheduler can see that
> and it won’t run the Goroutine.

**推荐理由**：

1. 大概了解线程和协程的一些区别
2. 有机会复习或者了解操作系统的一些基本概念
