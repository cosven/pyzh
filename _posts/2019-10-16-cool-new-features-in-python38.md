---
layout: post
title: Cool New Features in Python 3.8
date: 2019-10-16 13:30:00 +0800
tags: python release
---

**推荐理由**

算是新闻类文章吧，对每个 feature 有比较易懂的描述，可以从中看出一些 Python
语言的发展大方向，还是值得一读的。
<!--more-->

[原文链接](https://realpython.com/python38-new-features/)

shared by @cosven

------------

### 个人读后梳理

`f-strings` 功能已经丰富到这种程度了，还是有点吃惊。 

```python
>>> f"{name.upper()[::-1] = }"
"name.upper()[::-1] = 'CIRE'"
```

另外，从实际问题出发来解读 features（个人观点）

1. 从 *positional-only arguments* 的 [PEP](https://www.python.org/dev/peps/pep-0570/#motivation)，
可以看出它是是对 *工程实践* 的一些总结：将“约定"转换为具体的语法，降低误用 API 可能性。
2. *More Precise Types* 说明官方对 typing 还是非常重视的，这也算是工程实践吧
3. *math and statistics* 的改进应该是 Python 在科学计算领域广泛使用的体现
