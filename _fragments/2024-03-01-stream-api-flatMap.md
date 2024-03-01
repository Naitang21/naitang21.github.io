---
layout: fragment
title: Stream API flatMap()
tags: Java
description: Stream API .flatMap()
keywords: Java
typora-root-url: ..
---

`stream().flatMap` 是 Java 8 中 Stream API 提供的一个操作，用于将流中的每个元素映射为一个流，然后将所有生成的流扁平化为一个新的流。

具体来说，`flatMap` 方法接受一个函数作为参数，该函数将流中的每个元素映射为一个流。然后，`flatMap` 方法将所有生成的流组合成一个新的流，将每个流的元素平铺在一起。

使用示例：

```java
List<List<String>> list = Arrays.asList(
    Arrays.asList("apple", "banana"),
    Arrays.asList("orange", "grape"),
    Arrays.asList("melon", "pineapple")
);

List<String> flattenedList = list.stream()
    .flatMap(Collection::stream)
    .collect(Collectors.toList());

System.out.println(flattenedList);
```

在上述示例中，我们有一个包含多个列表的列表 `list`，每个列表中包含一些水果。通过 `stream().flatMap(Collection::stream)`，我们将每个子列表转换为一个单独的流，并最终将所有生成的流合并为一个新的流。最后，我们使用 `collect` 方法将扁平化后的元素收集到一个新的列表 `flattenedList` 中，并打印结果。

通过使用 `stream().flatMap`，我们可以将多个嵌套的集合转换为一个平铺的流，以便于后续的处理和操作。
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4NzMxODA4MjBdfQ==
-->