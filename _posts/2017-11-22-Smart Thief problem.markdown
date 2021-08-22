---
layout: article
title: Smart Thief 问题
date: 2017-11-22 19:27:52 +0800
categories: 算法
tag: 算法
---

* content
{:toc}

问题：  

<!-- more -->
![这里写图片描述](/images/Smart Thief problem_1.png)

实验室的老师发在群里的问题，不知道出处，下面给出一些自己的解答：

**方法一：整数规划（只是想求一个结果）**  
建模：  
将各房间看成一个变量Xi：X1，X2，…X12  
权重为每个房间的profit：W[i]  
目标：最大化所偷房间的权重和  
限制条件：  
X1+X2<=1,  
X2+X3<=1,  
…  
X12+X1<=1  
Xi属于{0,1}  
（0,1）整数规划问题可以借助excel或其他的一些软件来解，这里采用excel：  
![这里写图片描述](/images/Smart Thief problem_2.png)

**方法2：动态规划**  
![这里写图片描述](/images/Smart Thief problem_3.png)  
如图所示，从上至下，设共有n个房间，形成一个n个数的序列，i表示第i个房间，每个房间的profit为w[i]，Fi表示前i个数的最优收获，则对于第i个房间有两种可能，最优收获方案包括i或不包括i，当i<n时，前i个数中的第一个数和最后一个数不相邻，则有Fi=max（w[i]+F(i-2),F(i-1)）,当i=n时，情况有点特殊，即Fi=max（w[i]+F’(i-2),F[i-1]）,因为这时第n个数与第一个数实际上是相邻的，所以F’(i-2)实际上表示从第二个数开始到第i-2个数的最优方案，所以可以实现一个F函数从第一个数开始递推得到第i个数的最优方案，主函数调用两次该函数求最优，一次是求从第一个数到第n-1个数的最优解，第二次调用时第二个数到第n-2个数的最优解，然后将前者的值与后者加上w[n]的值进行对比。  
F函数总是由前两个状态的值得到第三个状态的解，如果只需要求得最大利润，相当于O(N)的时间复杂度，如果需要求最优方案，则需要维护每次求得的子问题的最优方案的值。  
下面给出了一个简单的C++代码，但是在维护最优方案值上不够高效，时间复杂度为O（N^2）  
(后面想到一种方法，不需要像下面代码那样每次对前两个最优方案的数组进行拷贝，可以实现一个二维数组a[n][n],a[i][j]=0或1，表示第i个数在前j个数的最优方案中是否被包含)

    
    
    #include <vector>
    #include <string>
    #include <algorithm>
    #include <iostream>
    
    using namespace std;
    
    //input:profit array,number of rooms;
    //output:step[],maxprofit;
    
    //step[n] step[i]=0 0r 1, means choose to steal or not respectively
    
    int Max_profit_range(vector<int> profit,vector<int> &step)  //attain the maximum profit and the stepof the input profit array
        {
            int n = profit.size();
            int k1 = profit[0]; 
            int k2,k3;
            if (n == 1)    //n为1的特殊情况
            {
                step[0] = 0;
                return profit[0];
            }
            vector<int> s1(n);
            vector<int> s2(n);
            vector<int> s3(n);
            int maxprofit = 0;
            s1[0] = 1;
            if (profit[0] >= profit[1])
            { 
                s2[0] = 1; 
                s2[1] = 0;
                k2 = profit[0];
            }
            else 
            {
                s2[0] = 0;
                s2[1] = 1;
                k2 = profit[1];
            }
            for (int i = 2; i < n; i++)   
            {
                if (profit[i] + k1 >= k2)  //逐渐向后递推，由前两个状态的值得到第三个状态的值
                {
                    s1[i] = 1;
                    k3 = profit[i] + k1;
                    s3 = s1;
                }
                else
                {
                    k3 = k2;
                    s3 = s2;
                }
                k1 = k2;
                k2 = k3;
                s1 = s2;
                s2 = s3;
            }
            step =s2;
            return k3;
        }
    
    void Max_profit(vector<int> profit)
        {
            int n = profit.size();
            int max_profit=0,step;
            if (n <= 3)
            {
                for (int i = 0; i < n; i++)
                {
                    if (max_profit < profit[i])
                    {
                        max_profit = profit[i];
                        step = i;
                    }
                }
                cout << "the maximum profit is: " << max_profit << endl;
                cout << "the step is:" << step+1 << ":" << profit[step] << endl;
                return;
            }
            auto it1 = profit.begin();
            auto it2 = profit.end();
            vector<int> profit1(it1 + 1, it2 - 2);
            vector<int> profit2(it1, it2 - 1);
            vector<int> step1(n,0),step2(n,0),step3(n,0);
            int k1, k2; 
            k1=profit[n-1]+Max_profit_range(profit1, step1);
            k2=Max_profit_range(profit2, step2);  //调用两次函数，将结果进行对比
            if (k1>=k2)
            {
                cout << "the maximum profit is " << k1 << endl;
                cout << "the step is:" << endl;
                step3.insert(step3.begin()+1,step1.begin(),step1.end());
                step3[0] = 1;
            }
            else
            {
                cout << "the maximum profit is " << k2 << endl;
                cout << "the step is:" << endl;
                step3=step2;
                step3.insert(step3.end(), 0);
            }
            for (int i = 0; i < n; i++){
                if (step3[i] == 1)cout << i+1 << ":" << profit[i] << endl;
            }
        }
    
    
    int main()
    {
        vector<int> profit{ 89, 55, 37, 6, 64, 99, 11, 23, 76, 4, 65, 9};
        Max_profit(profit);
        system("PAUSE");
        return 0;
    }

结果输出  
![这里写图片描述](/images/Smart Thief problem_4.png)

