---
layout: post
title: Python Attribute Access and the Descriptor Protocol
date: 2019-10-17 14:10:00 +0800
tags: python descriptor attribute
---

**推荐理由**

文章不多不少地、清楚地解释了 `foo.bar` 的内部运行逻辑。以前也看过一些资料，
感觉写得都没有这个好懂。
<!--more-->

[原文链接](https://amir.rachum.com/blog/2019/10/16/descriptors/)

shared by @cosven

------------

### 个人读后梳理

文章有个大概的结论：`__getattribute__` 的内部实现逻辑如下

```python
def my_getattribute(self, item):
    if item in self.__class__.__dict__:
        print('Retrieving from self.__class__.__dict__')
        v = self.__class__.__dict__[item]
    elif item in self.__dict__:
        print('Retrieving from self.__dict__')
        v = self.__dict__[item]
    else:
        print('Retrieving from self.__getattr__')
        v = self.__getattr__(item)
    if hasattr(v, '__get__'):
        print("Invoking descriptor's __get__")
        v = v.__get__(self, type(self))
    return v
```
