---
layout: post
title: Static Analysis at Scale: An Instagram Story
date: 2019-09-10 08:00:00 +0800
tags: python static-analysis lint
---

**推荐理由**

非常硬核的一篇技术文章，值得阅读，也是技术博客的一个好的学习榜样。
文章从『背景 -> 方案对比 -> 确认方案 -> 方案应用 -> 应用遇到问题 -> 调整 -> 未来展望』，
讲的都非常清晰和易懂，其中也有干货。

[原文链接](https://instagram-engineering.com/static-analysis-at-scale-an-instagram-story-8f498ab71a0c?gi=68a0c09f9d35)

shared by @cosven

------------

### 个人读后梳理

文章先说了 Instagram 是个 Python 大厂，所以项目在一个大仓库里面，而且 Instagram 每天要发布好几十次，维持代码质量是一件非常有挑战的事情，那 Instagram 是怎样解决这个问题的呢？

Instangram 从几个方面下手（维持代码质量），Linting 就是一个方面。

接着说了为什么需要 Linting？
1. 开发者遭遇问题的时候，自己可能并没有意识到，Linting 可以帮助开发者发现并且诊断问题
2. 在成百上千的开发者中普及优秀思想变得越来越难

Linting 如果有用，那有哪些常见方法呢？
1. 基于正则 -> easy, but dumb
2. AST-based Lints（Pyre + Mypy）-> powerful, but complex

谈 AST 的时候，不免要谈 CST，毕竟这是 Instagran 的主角：它说本来的 CST 会有点复杂，而 AST 又损失了比较多的信息。Instagram 就弄了个 LibCST，综合了两者的优点。
LibCST 提供了一个类似 CST 这样的无损表示（lossless representation）（注：AST 是一种 IR intermediate representation），但是它也可以像 AST 一样，比较容易的解析出语义信息。

举个了例子，LibCST 如果优雅的检测重复判断，示例代码：

```
# value imports
from typing import TYPE_CHECKING
from util import helper_fn

# type-only imports
if TYPE_CHECKING:
    from circular_dependency import CircularType

if TYPE_CHECKING:  # Whoops! Duplicate type guard!
    from other_package import OtherType
```

对于这个例子，它们可以基于 LibCST 非常容易了写一个 linting 规则，它给了例子（这里不贴上来了）。

这里才是文章的一半，这文章有点长呀...

接着讲它们是怎样用 LibCST 来实现 Linting Rules，在这个实践过程中，它们又经历了几个阶段
1. 初期：简单粗暴，使用 single visitor 模式。但是随着 rule 变多，这种模式很难维护
2. 解决初期遇到的困难：参考 ESLint 的设计，它们开发了一个中心化的 visitor registry
（这个部分没看太懂）

Lint 太吵（想想大家都诟病的 Pylint），它们一方面把严重的问题给高亮；另外，开发了 auto-fixer 功能。

Codemods: 自动修复代码，比如自动给代码加 type hint；修改差的函数名。

最后说基于 scope analysis 可以做更高级的代码修改。

最后总结：

> Finding the code we want to modify is often more important than the modification itself.
