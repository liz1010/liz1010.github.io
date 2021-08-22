---
layout: article
title: LeetCode-Reverse Integer
date: 2017-09-29 16:27:59 +0800
categories: 算法
tag: 算法
---

* content
{:toc}

原题：

<!-- more -->

> Reverse digits of an integer.  
>  **Example1** : x = 123, return 321  
>  **Example2** : x = -123, return -321
>
> **Note:**  
>  The input is assumed to be a 32-bit signed integer. Your function should
> return 0 when the reversed integer **overflows**.

思路：关键是溢出的问题，32位数表示的范围为：-2^31—2^31-1，INT_MAX=2^31-1，INT_MIN=-INT_MAX-1，关于表示范围的疑问，可参考博客：<https://www.sigmainfy.com/blog/2s-complement-int-max-int-min-difference.html>，采用long long整形来表示数以防溢出报错。注意：正负数不必区分，可以自己找几个数试验一下。

    
```c++
class Solution {
public:
    int reverse(int x){
        long long res=0;
        while(x!=0){
            res=10*res+x%10;
            x=x/10;
        }
        return (res>INT_MAX || res<INT_MIN)? 0:res;
    }
};
```

