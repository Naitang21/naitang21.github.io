---
layout: post
title: 拼写单词
categories: leetcode
description: 拼写单词--力扣题解
keywords: leetcode
typora-root-url: ..
---

﻿题目描述：
给你一份『词汇表』（字符串数组） words 和一张『字母表』（字符串） chars。

假如你可以用 chars 中的『字母』（字符）拼写出 words 中的某个『单词』（字符串），那么我们就认为你掌握了这个单词。

注意：每次拼写（指拼写词汇表中的一个单词）时，chars 中的每个字母都只能用一次。

返回词汇表 words 中你掌握的所有单词的 长度之和。
![在这里插入图片描述](/images/posts/2023-08-22-Spell-words/db38c280908740c389dcca1ed4ba9d8e.png)
方法一：
我的思路：
把words中的每一个字符串拿出来，转换成字符数组，查看每一个字符是否存在于chars中，如果存在，则在chars中移除该字符。
如果words中的字符串的每一个都存在于chars中，则计算该字符串的长度
该方法为暴力解法，执行时间较长，而且在不断的申请和释放空间。

```
class Solution {
    public int countCharacters(String[] words, String chars) {
          if (words.length==0 || chars.length()==0){
            return 0;
        }

        int count = 0;
        int flag ;
        String s;
        for (int i = 0; i < words.length; i++) {
            flag=1;
            s = chars;
            char[] c = words[i].toCharArray();
            for (int j=0;j<c.length;j++){
                int index = s.indexOf(c[j]);
                if (index==-1){
                    flag=0;
                    break;
                }else {
                    s=s.substring(0, index)+s.substring(index+1);
                }
            }
            if (flag==1){

                count = count+c.length;
            }

        }

        return count;
    }
}
```

看了题解之后，学到了以下方法
方法二：哈希表计数
![在这里插入图片描述](/images/posts/2023-08-22-Spell-words/fff187d866714777b45463f2f52af87b.png)

```
class Solution {
    public int countCharacters(String[] words, String chars) {
        Map<Character, Integer> charsCnt = new HashMap<Character, Integer>();
        int length = chars.length();
        for (int i = 0; i < length; ++i) {
            char c = chars.charAt(i);
            charsCnt.put(c, charsCnt.getOrDefault(c, 0) + 1);
        }
        int ans = 0;
        for (String word : words) {
            Map<Character, Integer> wordCnt = new HashMap<Character, Integer>();
            int wordLength = word.length();
            for (int i = 0; i < wordLength; ++i) {
                char c = word.charAt(i);
                wordCnt.put(c, wordCnt.getOrDefault(c, 0) + 1);
            }
            boolean isAns = true;
            for (int i = 0; i < wordLength; ++i) {
                char c = word.charAt(i);
                if (charsCnt.getOrDefault(c, 0) < wordCnt.getOrDefault(c, 0)) {
                    isAns = false;
                    break;
                }
            }
            if (isAns) {
                ans += word.length();
            }
        }
        return ans;
    }
}
```
![img](/images/posts/2023-08-22-Spell-words/49c80446d9ab4b95922148f503dd666a.png)