---
layout: article
title: 算法复杂度笔记
date: 2016-09-29 17:17:43 +0800
categories: 算法
tag: 算法
---

* content
{:toc}

## **空间复杂度S(n)**

根据算法写成的程序在执行时占用存储单元的长度。这个长度往往与输入数据的规模有关。空间复杂度过高的算法可能导致使用的内存超限，造成非正常中断。

<!-- more -->

## **时间复杂度T(n)**

根据算法写成的程序在执行时耗费时间的长度。这个长度往往也与输入数据的规模有关。时间复杂度过高的低效算法可能导致我们在有生之年都等不到运行结果。

## **算法评价标准**

在分析一般算法的效率时，我们经常关注的是下面两种复杂度：  
最坏情况复杂度  Tworst(n)  
平均复杂度  Tavg(n)

Tavg(n)≤Tavg(n)

## **算法度分析小窍门**

![这里写图片描述](/images/The algorithm complexity notes_1.png)

## **举例**

    
    
    void printN ( int N )
    { if ( N ){
         printN( N-1 );
         printf("%d\n", N );
      }
      return;
    }

![空间复杂度](/images/The algorithm complexity notes_2.png)

## **算法度排序**

![这里写图片描述](/images/The algorithm complexity notes_3.png)

![这里写图片描述](/images/The algorithm complexity notes_4.png)

