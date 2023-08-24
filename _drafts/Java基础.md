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

## `List<int>`或`List<String>`等，拼接元素并添加“，”

- 遍历List获取元素，使用StingBuilfer拼接字符串
- 使用stream API

## JAVA枚举

- 获取枚举的索引值

```
枚举类.class.getEnumConstants()[枚举索引]
```

- 根据索引值获取枚举值

```
枚举值.ordinal()
```

## 将String中的每一个字符转换成`List<String>`的每一个元素

- ```
  List<String> conmmandList = Stream.iterate(0, n -> ++n).limit((commands.length()))
              .map(n -> String.valueOf(commands.charAt(n)))
              .collect(Collectors.toList());
  ```

- ```
  List<String> conmmandList =Stream.of(commands.split(""))
              .map(n->String.valueOf(n))
              .collect(Collectors.toList());
  ```

## 拼接字符串时的换行

`System.lineSeparator() `

## 统计List中字符的重复次数

- - 先转成Map，再转回List

    ```
    private Map<String, Long> avertListToMap(List<String> wordList) {
        return wordList.stream().collect(Collectors.*groupingBy*(word->word,Collectors.*counting*()));
    }
    
    //map<字符，重复次数>转成List
    private List<Word> computeWordFrequencyAndSort(Map<String, Long> wordAmountMap) {
            return wordAmountMap.entrySet()
                    .stream()
                    .map(word -> new Word(word.getKey(), word.getValue().intValue()))
                    .sorted((word1, word2) -> word2.getWordCount() - word1.getWordCount())
                    .collect(Collectors.toList());
        }
    ```

  - 直接转成List

    ```
    private List<Word> countWordFrequency(List<String> wordList) {
            return wordList.stream()
                    .distinct()
                    .map(word -> new Word(word, Collections.frequency(wordList, word)))
                    .sorted((word1, word2) -> word2.getWordCount() - word1.getWordCount())
                    .collect(Collectors.toList());
        }
    ```

- String[] 转换为`List<String>`

```
private List<String> avertStringArrayToList(String[] words) {
        return Arrays.stream(words)
                .map(String::toString)
                .collect(Collectors.toList());
    }
```

- `List<Word>`转为String

  ```
  private String generateWordAndFrequency(List<Word> wordList) {
          return wordList.stream()
                  .map(word -> word.getValue() + " " + word.getWordCount())
                  .collect(Collectors.joining("\n"));
      }
  ```

  

## JAVA8-Stream API

1. 获取流

   1. 常见的容器Collection

      `Collection.stream()`

      `Collection.parallelStream()`

      `Arrays.stream(T arrray)  or Stream.of()`

   2. IO

      `java.nio.file.Files.walk()`

      `java.io.BufferedReader.lines()`

   3. 从无限大的数据源中产生流

      `Random.ints()`

   4. 基本数据类型

      `IntStream`

      `LongStream`

      `DoubleStream`

2. 流的操作类型

   1. Intermediate中间操作，可以有多个（惰性化lazy--仅调用方法，没有开始流的遍历）

      ```
      map (mapToInt, flatMap 等)、 filter、 distinct、 sorted、 peek、 limit、 skip、 parallel、 sequential、 unordered
      ```

   2. terminal终结操作，只能有一个，流的最后一个操作

      ```
      forEach、 forEachOrdered、 toArray、 reduce、 collect、 min、 max、 count、 anyMatch、 allMatch、 noneMatch、 findFirst、 findAny、 iterator
      ```

3. 例子

   1. 将List中所有字母转换为大写

      ```
      List<String> words=Arrays.asList("a","b","c");
      List<String> upperWords=words.stream().map(String::toUpperCase)
                                            .collect(Collectors.toList());
      
      ```

   2. flatmap扁平化映射：将多个`stream`连接成一个`stream`，比如数组降维

      ```
      List<List<Integer>> ints=new ArrayList<>(Arrays.asList(Arrays.asList(1,2),
                                                Arrays.asList(3,4,5)));
      List<Integer> flatInts=ints.stream().flatMap(Collection::stream).
                                             collect(Collectors.toList());
      
      ```

   3. 获取所有大于18岁的学生

      ```
      List<Student> studentNames = students.stream().filter(s->s.getAge()>18)
                                                    .collect(Collectors.toList());
      ```

   4. `distinct`是去重操作,它没有参数

   5. `sorted`排序操作，默认是从小到大排列，`sorted`方法包含一个重载，使用`sorted`方法，如果没有传递参数，那么流中的元素就需要实现`Comparable<T>`方法，也可以在使用`sorted`方法的时候传入一个`Comparator<T>`

      ```
      //以年龄排序
      students.stream().sorted((s,o)->Integer.compare(s.getAge(),o.getAge()))
                                        .forEach(System.out::println);;
            
            or
      //以年龄排序 
      students.stream().sorted(Comparator.comparingInt(Student::getAge))
                                  .forEach(System.out::println);;
                                  
                                  or
                                  //以姓名排序
      students.stream().sorted(Comparator.comparing(Student::getName)).
                                forEach(System.out::println);
      
      
      ```

   6. `peek`有遍历的意思，和`forEach`一样，但是它是一个中间操作，`peek`接受一个消费型的函数式接口

      ```
      //去重以后打印出来，然后再归并为List
      List<Student> sortedStudents= students.stream().distinct().peek(System.out::println).
                                                      collect(Collectors.toList());
      ```

   7. `limit`裁剪操作，和`String::subString(0,x)`有点先沟通，`limit`接受一个`long`类型参数，通过`limit`之后的元素只会剩下`min(n,size)`个元素，`n`表示参数，`size`表示流中元素个数

      ```
      //只留下前6个元素并打印
      students.stream().limit(6).forEach(System.out::println);
      ```

   8. `skip`表示跳过多少个元素，和`limit`比较像，不过`limit`是保留前面的元素，`skip`是保留后面的元素

      ```
      //跳过前3个元素并打印 
      students.stream().skip(3).forEach(System.out::println);
      
      ```

   9. `forEach`是终结操作的遍历，操作和`peek`一样，但是`forEach`之后就不会再返回流

      ```
      //遍历打印
      students.stream().forEach(System.out::println);
      ```

   10. 默认的`toArray()`返回一个`Object[]`，也可以传入一个`IntFunction<A[]> generator`指定数据类型

       ```
        Student[] studentArray = students.stream().skip(3).toArray(Student[]::new);
       ```

   11. max/min即找出最大或者最小的元素, 必须传入一个`Comparator`

   12. `count`返回流中的元素数量

       ```
       long  count = students.stream().skip(3).count();
       ```

   13. reduce为归纳操作，主要是将流中各个元素结合起来，它需要提供一个起始值，然后按一定规则进行运算，比如相加等，它接收一个二元操作 BinaryOperator函数式接口。从某种意义上来说，sum,min,max,average都是特殊的reduce

       1. reduce包含3个重载

          ```
          T reduce(T identity, BinaryOperator<T> accumulator);
          
          Optional<T> reduce(BinaryOperator<T> accumulator);
          
           <U> U reduce(U identity,
                           BiFunction<U, ? super T, U> accumulator,
                           BinaryOperator<U> combiner);
          
          ```

          2. reduce两个参数和一个参数的区别在于有没有提供一个起始值，如果提供了起始值，则可以返回一个确定的值，如果没有提供起始值，则返回Opeational防止流中没有足够的元素。

       long count = integers.stream().reduce(Integer::sum).get();


   14. anyMatch\ allMatch\ noneMatch测试是否有任意元素\所有元素\没有元素匹配表达式，他们都接收一个推断类型的函数式接口：`Predicate`

       ```
        boolean test = integers.stream().anyMatch(x->x>3);
       ```

       

   15. findFirst、 findAny获取元素，这两个`API`都不接受任何参数，`findFirt`返回流中第一个元素，`findAny`返回流中任意一个元素。

       ```
       int foo = integers.stream().findAny().get();
       ```

   16. collect收集操作，基本上所有的流操作最后都会使用它

       `collect`包含两个重载：一个参数和三个参数

       ```
        <R> R collect(Supplier<R> supplier,
                         BiConsumer<R, ? super T> accumulator,
                         BiConsumer<R, R> combiner);
       
       <R, A> R collect(Collector<? super T, A, R> collector);
       
       Supplier:用于产生最后存放元素的容器的生产者
       accumulator:将元素添加到容器中的方法
       combiner：将分段元素全部添加到容器中的方法
       ```

       

       ```
       一般来说，只有一个参数的collect，我们都直接传入Collectors中的方法引用即可
       List<Integer> = integers.stream().collect(Collectors.toList());
       
       Collectors中包含很多常用的转换器。toList(),toSet()等。
       Collectors中还包括一个groupBy()，他和Sql中的groupBy一样都是分组，返回一个Map
       
       //按学生年龄分组
       Map<Integer,List<Student>> map= students.stream().
                                       collect(Collectors.groupingBy(Student::getAge));
                                       
       groupingBy可以接受3个参数，分别是
       
       第一个参数：分组按照什么分类
       第二个参数：分组最后用什么容器保存返回（当只有两个参数是，此参数默认为HashMap）
       第三个参数：按照第一个参数分类后，对应的分类的结果如何收集
       有时候单参数的groupingBy不满足我们需求的时候，我们可以使用多个参数的groupingBy
       
       //将学生以年龄分组，每组中只存学生的名字而不是对象
       Map<Integer,List<String>> map =  students.stream().
       collect(Collectors.groupingBy(Student::getAge,Collectors.mapping(Student::getName,Collectors.toList())));
       
       toList默认生成的是ArrayList,toSet默认生成的是HashSet，如果想要指定其他容器，可以如下操作
        students.stream().collect(Collectors.toCollection(TreeSet::new));
       
       Collectors还包含一个toMap，利用这个API我们可以将List转换为Map
         Map<Integer,Student> map=students.stream().
                                  collect(Collectors.toMap(Student::getAge,s->s));
       
       值得注意的一点是，IntStream，LongStream,DoubleStream是没有collect()方法的，因为对于基本数据类型，要进行装箱，拆箱操作，SDK并没有将它放入流中，对于基本数据类型流，我们只能将其toArray()
       
       
       ```

       

4. 流的惰性操作

流的中间操作是惰性的，如果一个流操作流程中只有中间操作，没有终结操作，那么这个流什么都不会做，整个流程中会一直等到遇到终结操作操作才会真正的开始执行

在`Stream API`中，还包括一类`Short-circuiting`,它能够改变流中元素的数量，一般这类`API`如果是中间操作，最好写在靠前位置