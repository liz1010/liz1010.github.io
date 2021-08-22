---
layout: article
title: LeetCode-Longest Substring Without Repeating Characters
date: 2017-09-23 15:32:53 +0800
categories: 算法
tag: 算法
---

* content
{:toc}

原题：

<!-- more -->

> Given a string, find the length of the longest substring without  
>  repeating characters.
>
> **Examples:**  
>  Given “abcabcbb”, the answer is “abc”, which the length is 3.  
>  Given “bbbbb”, the answer is “b”, with the length of 1.  
>  Given “pwwkew”, the answer is “wke”, with the length of 3. Note that  
>  the answer must be a substring, “pwke” is a subsequence and not a  
>  substring.

可以利用set容器，注意此题容易出错的地方是：当发现有重复字符时，不是从这个重复字符开始重新计数，而是从原有字符串中被删掉的字符开始往后计。

    
```c++   
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        set<char> t;
        int l=0,r=0,length=0;
        while(r<s.size()){
            if(t.find(s[r])==t.end()){
                t.insert(s[r++]);
                length=max(length,(int)t.size());
            }
            else{
                t.erase(s[l++]);
            }
        }
        return length;
    }
};
```

