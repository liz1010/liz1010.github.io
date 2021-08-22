---
layout: article
title: LeetCode-Median of Two Sorted Arrays
date: 2017-09-25 18:34:36 +0800
categories: 算法
tag: 算法
---

* content
{:toc}

原题：

<!-- more -->

> There are two sorted arrays nums1 and nums2 of size m and n respectively.
> Find the median of the two sorted arrays. The overall run time complexity
> should be **O(log (m+n))**.
>
> **Example 1:** nums1 = [1, 3] nums2 = [2] The median is 2.0
>
> **Example 2:** nums1 = [1, 2] nums2 = [3, 4] The median is (2 + 3)/2 = 2.5

- 解法一：  
二分搜索，复杂度O ( log(min(m,n)) )，特别注意边界条件

left_part| right_Part  
---|---  
A[0], A[1], … A[i-1]| A[i], A[i+1], … A[m]  
B[0], B[1], … B[j-1]| B[j], B[j+1], … B[n]  
  
需要满足：

> len(left_part)==len(right_part)  
>  max(left_part)<=min(right_part)
    
```c++   
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int m=nums1.size(),n=nums2.size();
        // if(m<=n){vector<int>& A=nums1;vector<int>& B=nums2;}
        // else {vector<int>& A=nums2;vector<int>& B=nums1;}
        if(m>n)return findMedianSortedArrays(nums2,nums1);
        int imin=0,imax=m,half_len=(m+n+1)/2;
        int i,j;
        int max_of_left=0,min_of_right=0;
        while(imin<=imax){
            i=(imin+imax)/2;
            j=half_len-i;
            if(i<m && b[j-1]>a[i])imin=imin+1;
            //if(i<m && b[j-1]>a[i])imin=i+1;
            else if(i>0 && a[i-1]>b[j])imax=imax-1;
            //else if(i>0 && a[i-1]>b[j])imax=i-1;
            else{
                if(i==0)max_of_left = B[j-1];
                else if(j==0)max_of_left = A[i-1];
                else max_of_left = max(A[i-1],B[j-1]);

                if((m+n)%2==1)return max_of_left;

                if(i==m)min_of_right = b[j];
                else if(j==n)min_of_right = a[i];
                else min_of_right = min(a[i],b[j]);
                return (max_of_left + min_of_right)/2.0;
            }
        }
    }
};
```

- 解法二：  
采用归并将两个已排好序的数组放到一个数组中，找到其中位数。  
复杂度O ( m+n )

```c++   
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int m=nums1.size();
        int n=nums2.size();
        vector<int> marray(m+n);
        int i=0,j=0,k=0;
        while(i<m || j<n){
            if(i==m){marray[k++]=nums2[j++];continue;}
            if(j==n){marray[k++]=nums1[i++];continue;}
            if(nums1[i]<=nums2[j])marray[k++]=nums1[i++];
            else marray[k++]=nums2[j++];
        }
        return ((m+n)%2? marray[(m+n-1)/2]:(marray[(m+n)/2-1]+marray[(m+n)/2])/2.0); 
    }
};
```

