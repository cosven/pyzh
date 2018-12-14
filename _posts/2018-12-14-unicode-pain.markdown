---
layout: post
title: Pragmatic Unicode
date: 2018-12-12 10:02:00 +0800
tags: python unicode str bytes
---

**一句话概括**：非常好的描述了 Python 2 中字符编码的常见问题，并解释了为什么。

**推荐理由**：

看了这篇文章之后，会有一种「Python 中应该没有什么编码问题可以难倒自己了吧」的错觉。

<!--more-->

**摘要**

> Python 2 tries to be helpful when working with unicode and byte strings.
> If you try to perform a string operation that combines a unicode string with a byte string,
> Python 2 will automatically decode the byte string to produce a second unicode string,
> then will complete the operation with the two unicode strings.

[文章链接](https://nedbatchelder.com/text/unipain.html)

shared by @cosven

---------------------

### 个人读后感

个人感觉 Debug Python 编码问题主要是理解一下几个点

1. 知道自己是在用 Python 2 还是 Python 3
2. 编程世界中，各个系统一般都是通过 bytes 进行信息交换。
   拿到 bytes 后系统内部进行编解码，得到人可以阅读的 text
3. Python 3 中，str 是 unicode based str；Python 2 中，str 就是 bytes based str
4. 在 Python 2 中，解释器会隐式的为你做类型转换
    1. unicode.encode('xxx') => str
    2. str.decode('xxx') => unicode
    3. str.encode('xxx') 相当于 str.decode('ascii').encode('xxx')。ps: 一般是使用 ascii 进行隐式 decode，详情可以阅读文章。

5. 在 Python 3 中，没有 unicode 这个类型了
    1. str.encode('xxx') => bytes
    2. bytes.decode('xxx') => str



