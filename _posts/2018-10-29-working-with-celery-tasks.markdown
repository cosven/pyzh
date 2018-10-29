---
layout: post
title: Working with Asynchronous Celery Tasks – lessons learned
date:   2018-10-29 15:02:00 +0800
tags: python celery best-practice
---

**一句话概括**：Celery 的一些最佳实践

**推荐理由**：

1. 讲了编写 celery task 时需要注意的点
2. 个人过去也使用过 celery，阅读之后的感受是：
如果严格按照作者说的几个点来实现 celery task，会少踩很多坑！

<!--more-->

**摘要**

> 1. Use only simple types as task function arguments.
> 2. Always get the newest version of the object at task runtime.
> 3. Send task to the broker only when the function does not raise any exception and after the transaction is committed.
> 4. Make task idempotent to be sure that if the job is done only once.
> 5. Use “late acknowledgment” for idempotent tasks to protect them against incomplete execution.

[原文链接](http://www.zlovezl.cn/articles/python-using-variables-well/)

---------------

## 个人读后感

1. late ack 可以避免 celery prefetch 机制带来的任务排队问题
2. task 函数参数要尽量简单，不要(能)传 object：这个原则似乎适用于所有的任务队列系统
3. 任务要幂等，一定要幂等
