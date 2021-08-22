---
layout: article
title: LeetCode-Longest Palindromic Substring
date: 2017-09-27 20:46:13 +0800
categories: 算法
tag: 算法
---

* content
{:toc}

原题：

<!-- more -->

> Given a string s, find the longest palindromic substring in s. You may
> assume that the maximum length of s is 1000.
>
> **Example:**  
>  Input: “babad”  
>  Output: “bab”  
>  Note: “aba” is also a valid answer.
>
> **Example:**  
>  Input: “cbbd”  
>  Output: “bb”

- 解法一：  
以字符串中的每一个字符为中心向两边开始遍历，找到最长回文字符串，注意分奇偶两种情况。复杂度O(N^2)

    
```c++    
class Solution {
public:
    string longestPalindrome(string s) {
        int n=s.size();
        if(n==0 || n==1)return s;
        int i,l,r,k,curr_len,max_len=1;
        l=r=0;
        for(i=0;i<n;i++){
            if(s[i]==s[i+1]){
                curr_len=2;
                k=1;
                while((i-k)>=0 && (i+k+1)<n && s[i-k]==s[i+k+1]){
                    k++;
                    curr_len+=2;
                }
                if(curr_len>max_len){
                    max_len=curr_len;
                    l=i-k+1;
                    r=i+k;
                }
            }
            if(i>0){
                if(s[i-1]==s[i+1]){
                    curr_len=3;
                    k=2;
                    while((i-k)>=0 && (i+k)<n && s[i-k]==s[i+k]){
                        k++;
                        curr_len+=2;
                    }
                    if(curr_len>max_len){
                        max_len=curr_len;
                        l=i-k+1;
                        r=i+k-1;
                    }
                }
            }
        }
        return s.substr(l,r-l+1);
    }
};

//或者用函数实现（思路上更简单）
string expandAroundCenter(string s,int c1,int c2){
    int l=c1,r=c2;
    int n=s.length();
    while(l>=0 && r<=n && s[l]==s[r]){
        l--;
        r++;
    }
    return s.substr(l+1,r-l-1);
}
class Solution{
public:
    string longestPalindrome(string s){
        int n=s.size();
        if(n==0 || n==1)return s;
        string longest=s.substr(0,1);
        for(int i=0;i<n-1;i++){
            string p1=expandAroundCenter(s,i,i);
            if(p1.size()>longest.size())longest=p1;
        string p2=expandAroundCenter(s,i,i+1);
        if(p2.size()>longest.size())longest=p2;
        }
        return longest;
    }
}
```

- 解法二：  
动态规划，复杂度O(N^2)，见图示，dp[j][i]表示区间[j,i]是否为回文串，是则为1，否则为0，当i==j时，肯定为1，i=j+1时，若s[i]==[j]，则为1，当i-j>=2时，除了判断s[j]==s[i]还需dp[j+1][i-1]==1,也即：  
dp[j][i]=1, if i==j;  
dp[j][i]=(s[j]==s[i]), if j=i+1;  
dp[j][i]=(s[j]==s[i] && dp[i+1][j-1]), if j>i+1

![这里写图片描述](/images/LeetCode-Longest回文字符串_1.png)

    
```c++
class Solution{
public:
    string longestPalindrome(string s){
        int n=s.size();
        vector<vector<int>> dp(n,vector<int>(n,0));
        int left=0,right=0,len=0;
        for(int i=0;i<n;i++){
            for(int j=0;j<i;j++){
                dp[j][i]=(s[i]==s[j] && (i-j==1 || dp[j+1][i-1]));
                if(dp[j][i] && len < i-j+1){
                    len=i-j+1;
                    left=j;
                    right=i;
                }
            }
            dp[i][i]=1;
        }
        return s.substr(left,right-left+1);
    }
}
```

- 解法三：  
马拉车算法：Manacher’s Algorithm，复杂度O(N)，如图：  
![这里写图片描述](/images/LeetCode-Longest回文字符串_2.png)  

可参考博客：  
<http://www.cnblogs.com/grandyang/p/4475985.html>  
<http://blog.csdn.net/dyx404514/article/details/42061017>（个人认为这篇博客更加简单易懂）

    
```c++  
class Solution{
public:
    string longestPalindrome(string s){
        string t ="$#";
        for(int i=0;i<s.size();i++){
            t+=s[i];
            t+='#';
        }
        vector<int> p(t.size(),0);
        int id=0,mx=0,resId=0,resMx=0;
        for(int i=0;i<t.size();i++){
            p[i]=mx>i?min(p[2*id-i],mx-i):1;
            while(t[i+p[i]]==t[i-p[i]])++p[i];
            if(mx<i+p[i]){
                mx=i+p[i];
                id=i;
            }
            if(resMx<p[i]){
                resMx=p[i];
                resId=i;
            }
        }
        return s.substr((resId-resMx)/2,resMx-1);
    }
}
```

