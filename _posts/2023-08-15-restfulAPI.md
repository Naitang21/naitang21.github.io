---
layout: post
title: Restful API
categories: RestfulAPI
description: Restful API
keywords: Restful API
typora-root-url: ..

---

## REST是什么意思？

Representational State Transfer
架构风格

## Resource指什么？

一切可命名事物的对象
Web服务接受与返回的互联网媒体类型
Company、User

## Representation指什么？

资源的载体
JSON，XML，YAM等

## 什么是State Transfer？如何实现？

对资源的操作
用Web服务在该资源上所支持的一系列请求方法（比如：POST，GET，PUT或DELETE）

## 常见的Http Method

GET	    请求指定的页面信息，并返回实体主体。
HEAD	类似于 GET 请求，只不过返回的响应中没有具体的内容，用于获取报头
POST	向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。POST 请求可能会导致新的资源的建立和/或已有资源的修改。
PUT	    从客户端向服务器传送的数据取代指定的文档的内容。
DELETE	请求服务器删除指定的页面。
CONNECT	HTTP/1.1 协议中预留给能够将连接改为管道方式的代理服务器。
OPTIONS	允许客户端查看服务器的性能。
TRACE	回显服务器收到的请求，主要用于测试或诊断。
PATCH	是对 PUT 方法的补充，用来对已知资源进行局部更新。

## 常见的Http response status

1**	信息，服务器收到请求，需要请求者继续执行操作
2**	成功，操作被成功接收并处理
3**	重定向，需要进一步的操作以完成请求
4**	客户端错误，请求包含语法错误或无法完成请求
5**	服务器错误，服务器在处理请求的过程中发生了错误

## practice

![image-20230824234754154](/images/posts/2023-08-15-restfulAPI/image-20230824234754154.png)

![image-20230824234843248](/images/posts/2023-08-15-restfulAPI/image-20230824234843248.png)