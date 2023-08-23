---
layout: post
title: Spring DATA JPA
categories: Spring
description: Spring Data JPA
keywords: Spring JPA
typora-root-url: ..
---

## 缓存机制

JPA默认开启缓存机制，当调用findById方法获取repository中的实体对象时，如果缓存中存在这个对象，则直接从缓存中获取。更新实体对象之后，即使不调用save方法，JPA检测到缓存中的实体对象更新后，会自动更新到数据库 。