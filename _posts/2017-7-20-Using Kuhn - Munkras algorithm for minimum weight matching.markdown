---
layout: article
title: 利用Kuhn-Munkras算法求最小权值匹配
date: 2017-07-20 19:11:31 +0800
categories: 算法
tag: 算法
---

* content
{:toc}



KM算法求的是基于带权二分图中完备匹配下的最大权值匹配。关于km算法的讲解网上资料比较丰富，此处就不详述啦。这里主要整理一些用KM算法求最小权值匹配的一些问题。

  * 在求最大权值匹配时，不存在的边的权值设为0。在求最小权值匹配时，可以考虑将对应的权值变为相反数，或者用一个很大的数减去权值，然后再来求最大权值匹配，最后将权值和取反即可。如果使用将对应的权值变为相反数的方法，则不存在的边的权值此时要设为INT_MAX（即，实际中求匹配时使用的是-INT_MAX），如此设置之后还需要特别注意溢出的问题， `if( !sy[j] && ((lx[i] + ly[j] - weight[i][j] )<inc)` 这一句对于带符号整型数可能会溢出，所以此句可以改成`if( !sy[j] && weight[i][j]!=-INT_MAX && ((lx[i] + ly[j] - weight[i][j] )<inc)`,即不予考虑不存在的边。

  * 注意，km算法求的是完备匹配，即x集中的点数m与y集中的点数n不一定相同，但m<=n，最终结果是给x集合中的每一个值都找到一个y中的匹配。

  * 如果一个y集合中的点最多可以对应n个x集合中的点，则可以将y中的点数拓展n倍，最后变成一一对应的关系。

    
```c++   
#include <iostream>  
#include <cstdio>  
#include <memory.h>  
#include <algorithm>   
#include <limits.h>

using namespace std;  
		
#define MAX 100  
		
int m,n;	//x集与y集的点数
int weight[MAX][MAX];           //边的权重  
int lx[MAX],ly[MAX];            //期望值，定点标号  
bool sx[MAX],sy[MAX];           //记录寻找增广路时点集x，y里的点是否搜索过  
int match[MAX];                 //match[i]记录y[i]与x[match[i]]相对应  
		
bool search_path(int u) {          //给x[u]找匹配,这个过程和匈牙利匹配是一样的  
	int v;
	sx[u]=true;		  
	for(v=0; v<n; v++){  
		if(!sy[v] &&lx[u]+ly[v] == weight[u][v]){	//对于还没搜索过的且在相等子图中的点  
			sy[v]=true;  //标记一下表示搜索过
			if(match[v]==-1 || search_path(match[v])){	//名花无主或者还能腾出个位置（使用递归）  
				match[v]=u;  
				return true;  
			}  
		}  
	}  
	return false;  
}  
		
int Kuhn_Munkras(bool max_weight){  //表示求最大匹配(1)还是最小匹配(0)
	int i,j,u,inc,sum;
	if(!max_weight){ //如果求最小匹配，则要将边权取反  
		for(i=0;i<m;i++)  
			for(j=0;j<n;j++)  
				weight[i][j]=-weight[i][j];  
	}  
	//初始化顶标，lx[i]设置为max(weight[i][j] | j=0,..,n-1 ), ly[i]=0;  
	for(i=0;i<m;i++){  
		lx[i]=-0x7fffffff;  
		for(j=0;j<n;j++)  
			if(lx[i]<weight[i][j])  
				lx[i]=weight[i][j];  
	}  
	for(j=0;j<n;j++)ly[j]=0;
	memset(match,-1,sizeof(match));  
	//不断修改顶标，直到找到完备匹配或完美匹配  
	for(u=0;u<m;u++){   //为x里的每一个点找匹配  
		while(1){  
			memset(sx,0,sizeof(sx));  
			memset(sy,0,sizeof(sy));  
			if(search_path(u))       //x[u]在相等子图找到了匹配,继续为下一个点找匹配  
				break;  
			//如果在相等子图里没有找到匹配，就修改顶标，直到找到匹配为止  
			//首先找到修改顶标时的增量inc, min(lx[i] + ly [i] - weight[i][j],inc);,lx[i]为搜索过的点，ly[i]是未搜索过的点,因为现在是要给u找匹配，所以只需要修改找的过程中搜索过的点，增加有可能对u有帮助的边  
			inc=0x7fffffff;  
			for(i=0;i<m;i++)
			{
				if(sx[i])		//x是搜索过的点
					for(j=0;j<n;j++)
					{
						if(!sy[j]&&((lx[i] + ly [j] - weight[i][j] )<inc)) inc = lx[i] + ly [j] - weight[i][j] ;	//y是未搜索过的点
					}
			}
					//找到增量后修改顶标，因为sx[i]与sy[j]都为真，则必然符合lx[i] + ly [j] =weight[i][j]，然后将lx[i]减inc，ly[j]加inc不会改变等式，但是原来lx[i] + ly [j] ！=weight[i][j]即sx[i]与sy[j]最多一个为真，lx[i] + ly [j] 就会发生改变，从而符合等式，边也就加入到相等子图中  
			if(inc==0)  cout<<"fuck!"<<endl;  //都无法求其次，简直不可理喻，所以找不到完备匹配
			for(i=0;i<m;i++){  
				if(sx[i])     
					lx[i]-=inc;		//所有已搜索过的x减少相同的量，便于给其他的x找其他的路径
			}
			for(i=0;i<n;i++){
				if(sy[i])  
					ly[i]+=inc;		//对应的ly[]加上inc使得Lx[]+Ly[]与weight[]始终保持一致
			}  
		}  
		
	}  
	sum=0;  
	for(i=0;i<n;i++)  
		if(match[i]>=0)  
			sum+=weight[match[i]][i];  
		
	if(!max_weight)  
		sum=-sum;  
	return sum;  
		
}


int main(){  
	int i,j;
	printf("请输入X集与Y集的点数：M,N\n");
	scanf("%d%d",&m,&n);  
	printf("请输入权重\n");
	for(i=0;i<m;i++)  
	for(j=0;j<n;j++)  
		scanf("%d",&weight[i][j]);
	printf("%d\n",Kuhn_Munkras(0));  
	for(i=0;i<n;i++)printf("%d ",match[i]);
	system("pause");  
	return 0;  
}  
```

  **一些重要概念的补充：**

  * 二分图：顶点分为两个集合X和Y，所有的边关联在两个顶点中，恰好一个属于集合X，另一个属于集合Y。
  * 最大匹配：图中包含边数最多的匹配称为图的最大匹配。（这个时候不涉及权值）
  * 完备匹配与完美匹配：`G=< V1, V2, E >，|V1|<=|V2|，M为G中的一个最大匹配，且|M|=|V1|，则称M为V1到V2的完备匹配，若|V2|=|V1|，则完备匹配即为完美匹配，若|V1|<|V2|，则完备匹配为G中的最大匹配。`
  * 匈牙利算法：用增广路求二分图的最大匹配。
  * KM算法：利用匈牙利算法求完备匹配下的 **最大权重** 匹配。



**参考博客：** 

[http://blog.csdn.net/zhangpinghao/article/details/12242823（代码参考该博客）](http://blog.csdn.net/zhangpinghao/article/details/12242823%EF%BC%88%E4%BB%A3%E7%A0%81%E5%8F%82%E8%80%83%E8%AF%A5%E5%8D%9A%E5%AE%A2%EF%BC%89)  
[http://philoscience.iteye.com/blog/1754498（个人认为对km算法讲解比较好）](http://philoscience.iteye.com/blog/1754498%EF%BC%88%E4%B8%AA%E4%BA%BA%E8%AE%A4%E4%B8%BA%E5%AF%B9km%E7%AE%97%E6%B3%95%E8%AE%B2%E8%A7%A3%E6%AF%94%E8%BE%83%E5%A5%BD%EF%BC%89)