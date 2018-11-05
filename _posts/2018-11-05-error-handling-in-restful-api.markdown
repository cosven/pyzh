---
layout: post
title: Restful API 中的错误处理
date:   2018-11-05 12:00:00 +0800
tags: REST API error-handling
---

**一句话概括**：REST API 的错误处理实践

**推荐理由**：

看这篇文章之前，个人有一个疑问：当 POST/PUT/DELETE 等 API 请求出错时，
服务端怎样将不同类型的错误信息完整准确的告诉客户端开发者或者用户？
这篇文章较好的解决了我的这个疑问。

<!--more-->

**摘要**

> 当 Restful API 需要抛出错误的时候，我们要考虑的是：这个错误应该包含哪些信息。
> 我们先看看 Github, Google, Facebook, Twitter, Twilio 的错误信息是怎样的。
> ...
> 观察这些结构可以发现它们都有一些共同的地方：

> - 都利用了 Http 状态码
> - 有些返回了业务错误码
> - 都提供了给用户看的错误提示信息
> - 有些提供了给开发者看的错误信息

[原文链接](https://scarletsky.github.io/2016/11/30/error-handling-in-restful-api/)

shared by @cosven

-------------------

## 个人读后感

较好的错误处理方法就是：ErrorType + ErrorMsg + 一个合适的 HTTP
 status code.

涉及表单的时候，经常会有一个 errors 字段来标记哪些字段不符合规则。
曾经看过一些 API 校验的时候，是一个一个字段检查的，遇到一个错误，
就直接返回错误信息，这对用户体验非常不好。
