---
title: 'int' object has no attribute 'value'
date: 2023-01-02 16:14:01.701
updated: 2023-01-02 16:14:01.701
url: /archives/intobjecthasnoattributevalue
categories: 
tags: bug合集 | python
---

**出错原因**
困难是tensorflow版本问题

**解决方法**
- 将`in_channels = inputs.shape[-1].value`改为
 `in_channels = inputs.shape.as_list()[-1]`

- 直接将 `.value` 去掉