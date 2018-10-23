---
layout: post
title: Web 技術中的 Session 是什麼？
date:   2018-10-23 14:26:00 +0800
tags: web session flask
---

**一句话概括**：介绍了 session 的历史，原理和实现

**推荐理由**：

1. 介绍了 session 的历史，可以引发读者的一些思考
2. 描述了两种 session 实现技术

<!--more-->

**摘要**

> 在 Web 的世界裡，Session 已經是被廣泛使用的一種技術，大多數的 Web 開發者，
> 肯定都能運用自如。在現今的各類 Web 應用程式的開發框架和工具中，
> Session 也已經被包裝成容易使用的模式，所以本文也就不再多討論 Session 怎麼去使用，
> 而是著重在 Session 的原理和實現上。要知道，無論是使用哪一種語言，這 Session 概念上都是通用的，沒有什麼不一樣。

[原文链接](http://fred-zone.blogspot.com/2014/01/web-session.html)

--------------------

## 扩展阅读资料

### 高并发下 cookie-based sessions 实现存在的问题

对 flask 有兴趣的朋友，读完上文之后可以看看这个问题：
[Flask session doesn't update consistently with parallel requests](https://stackoverflow.com/questions/52822914/flask-session-doesnt-update-consistently-with-parallel-requests>)
