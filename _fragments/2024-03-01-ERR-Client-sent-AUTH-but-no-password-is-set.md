---
layout: fragment
title: Redis连接报错：ERR Client sent AUTH, but no password is set
tags: Redis
description: Redis连接报错：ERR Client sent AUTH, but no password is set
keywords: Redis
typora-root-url: ..
---

启动项目时，Redis报错：`ERR Client sent AUTH, but no password is set`
这是因为Redis服务器没有设置密码，但是客户端发送的AUTH(Authentication)请求携带着密码，导致报这个错误。
解决方法：给Redis服务器设置密码
进入`redis-cli.exe`，查看是否设置密码：
```
auth password
```
如果报错，则说明并没有设置密码，那我们就可以配置密码：
```
config set requirepass password
```
使用这个方法配置的密码，当Redis服务器关闭时，就会失效。下一次还需要去配置。

**Refs:**
[# Redis连接报错：ERR Client sent AUTH, but no password is set](https://blog.csdn.net/u014026084/article/details/105767907)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAxMzA3MTU0MSwyMDcxNDUxMDldfQ==
-->