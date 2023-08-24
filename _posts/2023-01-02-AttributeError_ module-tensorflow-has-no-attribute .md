---
layout: post
title: module 'tensorflow' has no attribute 'ConfigProto'
categories: Python Bug
description: module 'tensorflow' has no attribute 'ConfigProto'
keywords: Python
typora-root-url: ..
---

**出错原因**
代码基于tensorflow=1.x，而系统中的tensorflow=2.x

**解决方法**
1. 将tensorflow版本将为1.x
2. 修改代码
如将
```python
session = tf.Session(config=config)
```
修改成
```python
session = tf.compat.v1.Session(config=config)
```
其他的代码也类似





