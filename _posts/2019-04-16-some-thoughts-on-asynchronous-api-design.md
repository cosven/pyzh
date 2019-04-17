---
layout: post
title: Some thoughts on asynchronous API design in a post-async/await world
date:  2019-04-16 22:21:00 +0800
tags: python asyncio API
---

**推荐理由**

作者对比了 asyncio 和 curio 这两个异步 I/O 库，描述了它们在设计上的区别，
并举例说明了这些区别给我们实际编程带来的影响，可以让读者对 Python 异步 I/O
世界有一个更加完整的认识，对编程实践也有一定的指导意义。

<!--more-->

**摘要**

> I've recently been exploring the exciting new world of asynchronous I/O
> libraries in Python 3 – specifically asyncio and curio.
> These two libraries make some different design choices.
> This is an essay that I wrote to try to explain to myself
> what those differences are and why I think they matter,
> and distill some principles for designing event loop APIs and asynchronous libraries in Python.
> This is a quickly changing area and the ideas here are very much still under development,
> so this text probably assumes all kinds of background knowledge and
> possibly that you live inside my head – but maybe you'll find it interesting anyway.

[原文链接](https://vorpus.org/blog/some-thoughts-on-asynchronous-api-design-in-a-post-asyncawait-world/)

shared by @cosven

--------------------------

### 个人观后感

这篇文章非常的长，内容围绕异步 I/O 库散开，讲了它的很多方面，从使用到 API 设计，
再到原理和设计初衷，都有涉及。我自己虽然基本看完了全文，但并没有全部吸收。
我相信自己如果以后继续使用 asyncio，就一定会来重读这篇文章。

个人不敢写太多总结，怕理解有误，下面是我目前读完的零碎感想
（不保证以下理解的正确性，欢迎讨论或者备注）：

asyncio 的实现即有 callback style， 也有 async/await style，
两种风格的混合给开发者和使用者读带来了许多麻烦。curio 作为一个没有历史包袱的库，
它里面就没有 callback，是纯 async/await。

作者认为纯 async/await 是大的趋势，asyncio 以后暴露出来的 API 可能也会是这样，
但目前，asyncio 还有许多 callback 风格的接口，Protocol 就是一点典型。
（所以按照我个人的理解，我们最好是使用 `event_loop.sock_sendall/recv/accept`
这一套接口，坑少，更符合直觉。而 Protocol/Transport/StreamWriter/StreamReader
这些接口虽然也都能用，但使用时得比较小心，比如作者说的背圧(backpressure)问题等）

由于 hybrid API 带来的一些问题，asyncio 实现时就需要考虑很多 edge case，
这对开发者和使用者都是一个挑战。
