---
layout: fragment
title: Optional.ofNullable判空
tags: Java
description: 
keywords: Java
mermaid: false
sequence: false
flow: false
mathjax: false
mindmap: false
mindmap2: false
---

处理可能为null的变量时，避免null检查以及空指针异常，可以使用
```
Optional.ofNullable(obj).ifPresent(obj不为null时的处理)
Optional.ofNullable(obj).orElse(obj为null时的处理)
Optional.ofNullable(obj).orElseThrow(obj为null时抛出的异常)
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwMjA5OTgyNTZdfQ==
-->