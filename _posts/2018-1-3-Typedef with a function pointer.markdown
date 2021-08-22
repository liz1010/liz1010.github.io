---
layout: article
title: typedef与函数指针
date: 2018-01-03 15:50:55 +0800
categories: C/C++
tag: C/C++
---

* content
{:toc}

### **typedef**

利用typedef声明一个新的类型名的方法是：

<!-- more -->

    
    
    1. 先按定义变量的方法写出定义语句（如int i;）。
    2. 将变量名换成新类型名（如将i换成COUNT）。
    3.   在最前面加typedef(如typedef int COUNT)。
    4. 然后可以用新类型名去定义变量。
    

以声明上述的数组类型为例来说明：

    
    
    1. 先按定义数组形式书写： int n[100];
    2. 将变量名n换成自己指定的类型名：int NUM[100];
    3. 在前面加上typedef，得到 typedef int NUM[100];
    4. 用来定义变量： NUM n;(n是包含100个整型元素的数组)。
    

关于typedef的几点说明：

    
    
    1. typedef可以声明各种类型名，但不能用来定义变量。用typedef可以声明数组类型、字符串类型，使用比较方便。
    2. 用typedef只是对已经存在的类型增加一个类型名，而没有创造新的类型。
    3. 当在不同源文件中用到同一类型数据（尤其是像数组、指针、结构体、共用体等类型数据）时，常用typedef声明一些数据类型，把它们单独放在一个头文件中，然后在需要用到它们的文件中用＃include命令把它们包含进来，以提高编程效率。
    4. 使用typedef有利于程序的通用与移植。有时程序会依赖于硬件特性，用typedef便于移植。
    

来自 <http://c.biancheng.net/cpp/biancheng/view/180.html>

### **decltype类型指示符**

选择并返回操作数的数据类型，在此过程中，编译器分析表达式并得到它的类型，却不实际计算表达式的值。

    
    
    decltype(f()) sum=x;
    const int ci=0, &cj=ci;
    decltype(ci) x=0;   //x类型为const int
    decltype(cj) y=x;  //y的类型是const int&，y绑定到变量x
    decltype(cj) z;      //错误：z是一个引用，必须初始化
    int i=42, *p=&i；
    decltype(*p) c;  //错误，c是int&，必须初始化

如果表达式的内容是解引用操作，则decltype将得到引用类型。解引用指针可以得到指针所指的对象，而且还能给这个对象赋值，因此，decltype（*p）的结果类型就是int&，而非int。

### **函数指针**

函数指针指向的是函数而非对象，要想声明一个指向函数的指针，只需要用指针替换函数名即可：

    
    
    bool lengthCompare(const string&, const string&)
    bool (*pf)(const string&, const string&);

pf指向的函数参数是两个conststring的引用，返回类型是bool类型

  * 使用函数指针

使用函数名时，函数自动转换为指针：

    
    
    pf=lengthCompare;
    pf=&lengthCompare;  //两者等价，取址符可选

此外也可以直接使用指向函数的指针调用该函数，无需提前解引用指针：

以下三种表达等价

    
    
    bool b1=pf("hello", "goodbye");
    bool b2=(*pf)("hello", "goodbye");
    bool b3= lengthCompare("hello", "goodbye");

Pf=0；或者pf=nullptr；表示pf不指向任何函数。

通过指针类型决定选用函数时，指针类型必须与函数中的参数类型，返回类型精确匹配。

  * 函数指针形参

虽然不能定义函数类型的形参，但是形参可以是指向函数的指针。

    
    
    void useBigger(const string &s1,const string &s2, bool(*pf)(const string &, const string &));
    void useBigger(const string &s1, const string &s2, boolpf(const string &, const string &));

将函数名作为实参使用，自动转换为指针

    
    
    useBigger(s1, s2, lengthCompare);

使用typedef与decltype简化表达：

    
    
    //Func Func2是函数类型
    typedef bool Func(const string &, const string &);
    typedef decltype(lengthCompare) Func2;
    
    //FuncP,FuncP2是指向函数的指针
    typedef bool (*FuncP)(const string &, const string &)；
    typedef decltype(lengthCompare) *FuncP2；

useBigger的等价声明：

    
    
    void useBigger(const string &s1, const string &s2, Func);
    void useBigger(const string &s1, const string &s2, FuncP2));

第一条中，编译器自动将Func表示的函数类型转换为指针。

返回指向函数的指针：

    
    
    using F=int（int*，int);   //F是函数类型，不是指针
    using PF=int(*)(int*,int);  //PF是指针类型
    F *f1(int);
    PF *f1(int);
    //等价于：
    int (*f1(int))(int *,int);

