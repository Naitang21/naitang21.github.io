---
layout: fragment
title: int object has no attribute 'value'
tags: Python Bug
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

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3NzIwODI0MV19
-->