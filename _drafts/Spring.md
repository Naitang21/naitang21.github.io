---
layout: post
title: template page
categories: [cate1, cate2]
description: some word here
keywords: keyword1, keyword2
typora-root-url: ..
mermaid: false
sequence: false
flow: false
mathjax: false
mindmap: false
mindmap2: false
---

## spring依赖注入

```
@Component  or @Repository
需要交给spring管理的类

需要使用spring管理的类A的类B
@Autowired or @Service
属性
```

```
@RequiredArgsConstructor
需要使用spring管理的类A的类B{
	private final 类A 命名；
}@RequiredArgsConstructor

```

