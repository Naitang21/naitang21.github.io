---
layout: fragment
title: Redis连接报错：ERR Client sent AUTH, but no password is set
tags: Redis
description: ## Redis连接报错：ERR Client sent AUTH, but no password is set
keywords: Redis
typora-root-url: ..
---

启动项目时，Redis报错：`ERR Client sent AUTH, but no password is set`
这是因为Redis服务器没有设置密码，但是客户端发送的AUTH(Authentication)请求携带着密码，导致报这个错误。
解决方法：给Redis服务器设置密码
方法一：
进入`redis-cli.exe`，查看是否设置密码：
```
auth m
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk4NjE0OTc4NV19
-->