---
title: AttributeError: module 'tensorflow' has no attribute 'ConfigProto'
date: 2023-01-02 15:47:15.446
updated: 2023-01-02 15:47:15.446
url: /archives/attributeerrormoduletensorflowhasnoattributeconfigproto
categories: 
tags: bug合集 | python
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





