---
layout: article
title: 一小段C++程序反映出的问题
date: 2017-12-31 12:02:07 +0800
categories: C/C++
tag: C/C++
---

* content
{:toc}


    #include<string>

<!-- more -->
    #include<iostream>
    
    using namespace std;
    
    class A{
    public:
    	A(int n){ value = n; }
    	A(const A& other){ value = other.value; }		
    	//直接调用other的私有成员，这是因为访问权限针对的是类而不是对象，所以在同一个类中，还是可以直接访问私有成员变量的
    	//注意拷贝构造函数的参数不能定义为A(A other)因为这样的话相当于传值，形参复制到实参就会调用拷贝函数，因此会在拷贝构造函数内调用拷贝构造函数，形成无休止的
    	//递归调用而导致栈溢出。
    	void print(){ cout << value << endl; }
    private:
    	int value;
    };
    
    
    
    void main(){
    	A a = 10;	//复制初始化，首先调用构造函数A(int n)函数创建一个临时对象，然后调用拷贝构造函数，把这个临时对象作为参数，构造对象a
    	A b = a;	//复制初始化，因为a本就存在，所以直接调用拷贝构造函数，构造对象b
    	b.print();
    	system("PAUSE");
    	return;
    }

  

这里涉及到的问题：

构造函数的参数设置

成员变量的访问权限是针对类而不是对象而言

构造函数的调用  

