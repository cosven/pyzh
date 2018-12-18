---
layout: post
title: What is the Python Global Interpreter Lock (GIL)?
date:  2018-12-18 09:20:00 +0800
tags: python GIL
---

**推荐理由**：

这篇文章简单明了的介绍了 GIL 产生的背景，是一篇挺不错的 GIL 入门文章
读完应该可以知道下面几个基础问题？

- 为何有 GIL？
- GIL 解决了什么问题？又带来了什么问题？
- 为何 GIL 一直被诟病，但却仍然存在？
- 怎样应对 GIL？

了解 GIL 底层原理可以看 [David Beazley: Understanding the Python GIL](https://youtu.be/Obt-vMVdM8s)

<!--more-->

**摘要**

> The Python Global Interpreter Lock or GIL, in simple words,
> is a mutex (or a lock) that allows only one thread to hold the control of
> the Python interpreter.
>
> This means that only one thread can be in a state of execution
> at any point in time. The impact of the GIL isn’t visible to developers
> who execute single-threaded programs, but it can be a performance bottleneck
> in CPU-bound and multi-threaded code.
>
> Since the GIL allows only one thread to execute at a time even
> in a multi-threaded architecture with more than one CPU core,
> the GIL has gained a reputation as an “infamous” feature of Python.
>
> In this article you’ll learn how the GIL affects the performance of
> your Python programs, and how you can mitigate the impact it might
> have on your code.

[原文链接](https://realpython.com/python-gil/)

shared by @cosven
