---
layout: fragment
title: Bean Validation
tags: Java
description: Bean Validation
keywords: Bean Validation
mermaid: false
sequence: false
flow: false
mathjax: false
mindmap: false
mindmap2: false
---

## 一些常用的注解：

- `@NotNull`: 被注释的元素必须不为null。
- `@Min(value)`: 被注释的元素必须是一个数字，其值必须大于等于指定的最小值。
- `@Max(value)`: 被注释的元素必须是一个数字，其值必须小于等于指定的最大值。
- `@Size(min=, max=)`: 被注释的元素的大小必须在指定的范围内。
- `@Digits(integer=, fraction=)`: 被注释的元素必须是一个数字，其值必须拥有最多指定位数的整数部分和最多指定位数的小数部分。
- `@Past`: 被注释的元素必须是一个过去的日期。
- `@Future`: 被注释的元素必须是一个将来的日期。
- `@Pattern(regex=,flag=)`: 被注释的元素必须符合指定的正则表达式。
- `@NotBlank`: 被注释的字符串必须非空，且至少包含一个非空白字符。
- `@NotEmpty`: 被注释的字符串的必须非空。
- `@Email`: 被注释的元素必须是电子邮箱地址。
- `@Positive`: 被注释的元素必须是正数。
- `@PositiveOrZero`: 被注释的元素必须是正数或0。
- `@Negative`: 被注释的元素必须是负数。
- `@NegativeOrZero`: 被注释的元素必须是负数或0。
- `@AssertTrue`: 被注释的元素必须为true。
- `@AssertFalse`: 被注释的元素必须为false。


## 多个字符串判断是否都非空且长度>1
`StringUtils.isNoneBlank` 是 Apache Commons Lang 库中的一个方法，它用于检查给定的一个或多个 `CharSequence`（如 `String` ）是否都非 null，且长度（除去首尾空白字符后）大于 0。

**例子**：

```
StringUtils.isNoneBlank("test"); // 返回 true
StringUtils.isNoneBlank(" test "); // 返回 true
StringUtils.isNoneBlank(" "); // 返回 false
StringUtils.isNoneBlank(""); // 返回 false
StringUtils.isNoneBlank((String) null); // 返回 false
StringUtils.isNoneBlank("test", " test "); // 返回 true
StringUtils.isNoneBlank("test", " ");// 返回 false
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc4ODY5NjU0N119
-->