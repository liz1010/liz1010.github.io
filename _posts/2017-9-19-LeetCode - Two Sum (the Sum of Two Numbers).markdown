---
layout: article
title: LeetCode-Two Sum（两数之和）
date: 2017-09-19 15:51:24 +0800
categories: 算法
tag: 算法
---

* content
{:toc}

原题：

<!-- more -->

> Given an array of integers, return indices of the two numbers such that they
> add up to a specific target. You may assume that each input would have
> exactly one solution, and you may not use the same element twice.
>
> **Example:**  
>  Given nums = [2, 7, 11, 15], target = 9,  
>  Because nums[0] +nums[1] = 2 + 7 = 9,  
>  return [0, 1].

- 解法一：两层循环遍历(100ms)

    
```c++   
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> element(2);
        int n=nums.size();
        int i,j;
        for(i=0;i<n;++i)
        {
            for(j=i+1;j<n;j++)
            {
                    if((nums[i]+nums[j])==target){
                    element[0]=i;
                    element[1]=j;
                    return element;  
                    }
            }
        }

    }
};
```

- 解法二：利用map查找提高效率(6ms)

    
```c++  
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int,int> m;
        vector<int> element(2);
        int n=nums.size();
        int i;
        for(i=0;i<n;++i)m[nums[i]]=i;
        for(i=0;i<n;++i)
        {
            int secnum=target-nums[i];
            if(m.count(secnum) && m[secnum]!=i])
            {
                element[0]=i;
                element[1]=m[secnum];
                return element;  
            }
        }

    }
};
```

