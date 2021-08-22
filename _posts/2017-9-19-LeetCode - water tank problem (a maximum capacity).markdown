---
layout: article
title: LeetCode-水箱问题（求最大容量）
date: 2017-09-19 11:31:19 +0800
categories: 算法
tag: 算法
---

* content
{:toc}

原题：

<!-- more -->

> Given n non-negative integers a1, a2, …, an, where each represents a point
> at coordinate (i, ai). n vertical lines are drawn such that the two
> endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together
> with x-axis forms a container, such that the container contains the most
> water.
>
> 要找到两条纵线，然后这两条线以及X轴构成的容器能容纳最多的水。

关键点：

  * 容量的高由两条边l与r中最短的那条决定，容量可表示为：min（l,r）*(r-l)；
  * 两条纵线l，r构成最大容量，令l < r，则l的左侧没有比l更高的线，r的右侧也没有比r更高的线；
  * 从两边向中间靠拢，当底减小时，只有高增大才有可能使容量变大；

代码：

```c++   
class Solution {
public:
    int maxArea(vector<int>& height) {
        int l=0;
        int r=height.size()-1;
        int k;
        int mArea=0;
        while(l<r){
            mArea=max(mArea,min(height[l],height[r])*(r-l));
            if(height[l]<=height[r]){
                k=l+1;
                while(k<r && height[k]<=height[l])k++;
                l=k;
            }
            else{
                k=r-1;
                while(k>l && height[k]<=height[r])k--;
                r=k;
            }
        }
    return mArea;
    }
};
```

再来思考一下如果是求最小容量呢？  
找到最短边然后找一条相邻的纵线就构成了最小容量哈哈~~

