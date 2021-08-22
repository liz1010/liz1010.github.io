---
layout: article
title: LeetCode-ZigZag Conversion
date: 2017-09-29 10:08:54 +0800
categories: 算法
tag: 算法
---

* content
{:toc}

原题：

<!-- more -->

> The string “PAYPALISHIRING” is written in a zigzag pattern on a given number
> of rows like this: (you may want to display this pattern in a fixed font for
> better legibility)  
>  ![这里写图片描述](/images/LeetCode-ZigZag Conversion_1.png)
>
> And then read line by line: “PAHNAPLSIIGYIR”  
>  Write the code that will take a string and make this conversion given a
> number of rows:  
>  string convert(string text, int nRows);  
>  convert(“PAYPALISHIRING”, 3) should return “PAHNAPLSIIGYIR”.

理解zigzag的含义：  
从上至下，再从下至上走之字形状，分析规律：numRows=5，第一行间隔8=5*2-2，第二行间隔：8-2,2  
第三行：8-4,4，以此类推。  
![这里写图片描述](/images/LeetCode-ZigZag Conversion_2.png)

    
  ```c++  
    class Solution {
    public:
        string convert(string s, int numRows) {
            if(numRows==1)return s;
            int n=s.size();
            int interval=numRows*2-2;
            int i,k=0;
            string res(n,' ');
            for(i=0;i<n;i+=interval){
                res[k++]=s[i];
            }
            for(i=1;i<numRows-1;i++){
                int inter=2*i;
                for(int j=i;j<n;j+=inter){
                    res[k++]=s[j];
                    inter=interval-inter;
                }
            }
            for(i=numRows-1;i<n;i+=interval){
                res[k++]=s[i];
            }
            return res;
        }
    };
```
