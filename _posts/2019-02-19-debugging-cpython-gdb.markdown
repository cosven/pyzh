---
layout: post
title: Debugging of CPython processes with gdb
date:  2019-02-19 11:02:00 +0800
tags: python debug gdb
---

**推荐理由**：

这篇文章讲述了怎样使用 GDB 来调试 CPython 进程，在讲述的过程中，
把 debug 遇到的常见问题和相关概念也拎了出来，信息量很大。

- 为什么使用 GDB?
- 使用 GDB 来调试 Python 进程有什么特殊之处？
- GDB 调试 Python 手把手教学，提醒了常见的坑?
- 教我们写一个 GDB 扩展来提升调试效率

<!--more-->

**摘要**

> [pdb](https://docs.python.org/3.5/library/pdb.html) has been,
> is and probably always will be the bread and butter of Python programmers,
> when they need to find the root cause of a problem in their applications,
> as it's a built-in and easy to use debugger. But there are cases,
> when pdb can't help you, e.g. if your app has got stuck somewhere,
> and you need to attach to a running process to find out why,
> without restarting it. This is where gdb shines.

[原文链接](https://www.podoliaka.org/2016/04/10/gg/)

shared by @cosven

---------------------

### 个人读后感

这篇文章中提到了 debug 时遇到的很多关键概念，并给出了链接：非常贴心。
这对我们扩展相关知识，形成知识网络很有用。比如：

> gdb allows one to take a [core dump](https://en.wikipedia.org/wiki/Core_dump) of a process and analyze it later.
> This is useful, when you don't want to stop the process for the duration of time,
> while you are introspecting its state, as well as when you do post-mortem debugging of a process that has already failed (e.g. crashed with a segmentation fault)


> However, [PyEval_EvalFrameEx](https://docs.python.org/2/c-api/veryhigh.html#c.PyEval_EvalFrameEx))
> looks interesting: it's a function of CPython, which executes bytecode of Python application level functions and,
> thus, has access to their state - the very state we are usually interested in.

之前，我也看过一个关于 Python DEBUG 的分享，感觉也挺有学习意义的
[我的Python进程怎么了](https://github.com/HZPUG/HZPUG.github.io/blob/master/lectures/2018-11-25/%E6%88%91%E7%9A%84Python%E8%BF%9B%E7%A8%8B%E6%80%8E%E4%B9%88%E4%BA%86.pdf)
