---
layout: post
title: int object has no attribute 'value'
categories: Python Bug
description: Python Bug
keywords: Python
typora-root-url: ..
---

**'int' object has no attribute 'value'**

**出错原因**
困难是tensorflow版本问题

**解决方法**

- 将`in_channels = inputs.shape[-1].value`改为
  `in_channels = inputs.shape.as_list()[-1]`

- 直接将 `.value` 去掉

