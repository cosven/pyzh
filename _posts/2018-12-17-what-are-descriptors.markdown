---
layout: post
title: Python 201 - What are descriptors?
date:  2018-12-17 09:40:00 +0800
tags: python descriptors
---

**推荐理由**：

这是一篇介绍 Python 描述器的文章：可以带读者认识描述器以及它背后的原理

1. 知道描述器在哪些地方有应用： `@property` `@classmethod`
2. 讲述了描述器协议
3. 描述器是怎样工作的
4. 文章末尾有一些相关阅读，看完这篇还没懂但又有兴趣的同鞋可以继续深入了解

<!--more-->

**摘要**

> Descriptors are pretty important because of all the places
> they are used in Python’s source code. They can be really useful
> to you too if you understand how they work. However,
> their use cases are pretty limited and you probably
> won’t be using them very often. Hopefully this chapter will have
> helped you see the descriptor’s usefulness and when you might
> want to use one yourself.

[原文链接](https://www.blog.pythonlibrary.org/2016/06/10/python-201-what-are-descriptors/)

shared by @cosven

---------------

### 个人读后感

以前多次遇到描述器，像 `lazy_property` 可能是最经典最常见的一个例子了。
但之前自己一直都有一些疑问：

1. 描述器是个啥？
2. 描述器和 property 是什么关系？
3. 什么场景可以用描述器？

在看完这篇文章以及一些零碎资料后，有了下面的感悟：

关于描述器是啥的问题？官方文档中有描述：
> ```
> descr.__get__(self, obj, type=None) -> value
> descr.__set__(self, obj, value) -> None
> descr.__delete__(self, obj) -> None
> ```
> That is all there is to it. Define any of these methods and an object
> is considered a descriptor and can override default behavior upon
> being looked up as an attribute.

人肉翻译一下，Python 有一个协议，实现了这个协议的就叫做描述器，文章中也有详细讲。
property 就是通过描述器协议实现的，它是一个描述器，它也是一个普通的类。
在 CPython 源码中，property 类是用 C 写的，但在 Python Doc 中也有一个纯 Python 实现：
[pure python property implementation](http://docs.python.org/2/howto/descriptor.html#properties)

另外在 CPython Objects/descobject.c 文件中有句话很有启发：
> Descriptors -- a new, flexible way to describe attributes

目前我觉得可以使用描述器的场景是：

- 一个类的 **许多** **属性** 都需要具备一种 **黑魔法**
- 不同类的某些属性都需要具备 **同一种** 黑魔法。property 就属于这种情景。

文章中还有一个总结：日常编码中，我们很少会自己写描述器；
但理解它，对我们理解 Python 基础有较大帮助。所以日常用不到的话，也不用慌。
