---
layout: fragment
title: Redis连接报错：ERR Client sent AUTH, but no password is set
tags: Redis
description: ## Redis连接报错：ERR Client sent AUTH, but no password is set
keywords: Redis
typora-root-url: ..
---

启动项目时，Redis报错：`ERR Client sent AUTH, but no password is set`
这是因为Redis服务器没有设置密码，但是客户端发送了AUTH(Authentication)
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzA0NzE1NzQ1XX0=
-->