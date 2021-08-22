---
layout: article
title: LeetCode-Add Two Numbers
date: 2017-09-21 19:36:54 +0800
categories: 算法
tag: 算法
---

* content
{:toc}

原题：

<!-- more -->

> You are given two non-empty linked lists representing two non-negative
> integers. The digits are stored in reverse order and each of their nodes
> contain a single digit. Add the two numbers and return it as a linked list.
>
> You may assume the two numbers do not contain any leading zero, except the
> number 0 itself.
>
> Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)  
>  Output: 7 -> 0 -> 8

注意：正常两数相加即是从最后一个数开始相加，向前进位，所以这一题只需要按照链表的正常顺序依次往后执行加法运算就好。

    
```c++
/**
    * Definition for singly-linked list.
    * struct ListNode {
    *     int val;
    *     ListNode *next;
    *     ListNode(int x) : val(x), next(NULL) {}
    * };
    */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode * s=new ListNode(-1);
        ListNode * head=s;
        int res=0,sum=0;
        while(l1||l2){
            if(l1){sum+=l1->val;l1=l1->next;}
            if(l2){sum+=l2->val;l2=l2->next;}
            sum+=res;
            ListNode* n=new ListNode(sum%10);
            res=sum/10;
            s->next=n;
            s=s->next;
            sum=0;
        }
        if(res)s->next=new ListNode(res);
        return head->next;
    }
};
```

