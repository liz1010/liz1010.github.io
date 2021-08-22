---
layout: article
title: strcpy/strlen/strcat/strcmp的实现
date: 2018-01-15 16:18:32 +0800
categories: C/C++
tag: C/C++
---

* content
{:toc}

刷到一道题：写出完整版的strcpy函数

<!-- more -->

![这里写图片描述](/images/The realization of strcpystrlenstrcatSTRCMP_1.png)

索性对相关函数进行一下整理：

## 1.字符串拷贝函数strcpy  

函数strcpy的原型是char* strcpy(char* des , const char* src)，des 和 src 所指内存区域不可以重叠且
des 必须有足够的空间来容纳 src 的字符串。

    
    
    #include<cassert>       //assert的定义
    #include<cstddef>       //NULL的定义
    char * strcpy(char * strDst, const char * strSrc)
    {
        assert((strDst != NULL) && (strSrc != NULL));
        char * address = strDst;
        while ((*strDst++ = *strSrc++) != 0);
        return address;
    }
    

要点：  
1\. strcpy在执行字符串的复制或追加过程中，不执行溢出检查  
2\. strcpy会拷贝’\0’，且在拷贝的过程中根据’\0’判断是否停止拷贝  
3\. 注意编程风格，变量的命名要规范  
4\. 源指针所指的字符串不能修改，应该声明为const  
5\. 要判断一下源指针与目的指针为空的情况，思维要严谨，这里使用assert  
6\. 需要使用临时变量保存目的字符串的地址，并返回该地址  
7\. 函数返回char *的目的是为了支持链式表达式，即strcpy可以作为其他函数的实参。

## 2.字符串长度strlen

    
    #include<cassert>
    #include<cstddef>
    size_t strlen(char * str)
    {
        assert(str != NULL);
        size_t len = 0;
        while ((*str++) != '\0')len++;
        return len;
    }

## 3.字符串拼接strcat  

函数strcat的原型是char* strcat(char* des, char* src)，des 和 src 所指内存区域不可以重叠且 des
必须有足够的空间来容纳 src 的字符串。

    
    
    #include<cassert>
    #include<cstddef>
    char * strcat(char * strDst, const char * strSrc)
    {
        assert((strDst != NULL) && (strSrc != NULL));
        char *address = strDst;
        while (*strDst != '\0')strDst++;
        while ((*strDst++ = *strSrc++) != '\0');
        return address;
    
    }

## 4.字符串比较strcmp  

函数strcmp的原型是int strcmp(const char *s1,const char *s2)。

  * 若s1==s2，返回零；
  * 若s1>s2，返回正数；
  * 若s1<s2，返回负数。

即：两个字符串自左向右逐个字符相比（按ASCII值大小相比较），直到出现不同的字符或遇\0为止。

    
    
    #include<cassert>
    #include<cstddef>
    int strcmp(const char * str1, const char * str2)
    {
        assert((str1 != NULL) && (str2 != NULL));
        while (*str1 == *str2)
        {
            if (*str1 == '\0')
                return 0;
            ++str1;
            ++str2;
        }
        return *str1 - *str2;
    }

## Ref
<https://songlee24.github.io/2015/03/15/string-operating-function/>