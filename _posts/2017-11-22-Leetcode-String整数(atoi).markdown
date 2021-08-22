---
layout: article
title: Leetcode-String to Integer (atoi)
date: 2017-11-22 17:29:26 +0800
categories: 算法
tag: 算法
---

* content
{:toc}

问题

<!-- more -->

> Implement atoi to convert a string to an integer.  
>  将一个字符串转化为整数

问题看似简单，实际上有许多需要注意的细节。  
要点：

  * 对特殊字符进行处理：空格字符，放在前面的0字符
  * 只有在数字0-9内的字符才能转化为整数，否则全部返回0
  * 正负号的问题：默认为正数，直接读取符号判断是否为正数还是负数
  * 边界的问题：去掉正负数之后，与INT_MAX(2^31-1=2147483647)的值进行对比，越界则直接返回INT_MAX或者INT_MIN（关于溢出的问题，可以参考博客：<https://www.sigmainfy.com/blog/2s-complement-int-max-int-min-difference.html>

    
    ```c++
    class Solution {
    public:
        int myAtoi(string str) {
            int base=0,sign=1,i=0;
            while(str[i]==' ')i++;
            if(str[i]=='-'||str[i]=='+')
                sign=1-2*(str[i++]=='-');
            while(str[i] >= '0' && str[i] <= '9')
            {
                if(base>INT_MAX/10 || (base==INT_MAX/10 && str[i]-'0'>7))
                {
                   if(sign==1)return INT_MAX;
                   else return INT_MIN;
                }
                base=base*10+(str[i++]-'0');
    
            }
            return base*sign;
    
        }
    };
    ```

