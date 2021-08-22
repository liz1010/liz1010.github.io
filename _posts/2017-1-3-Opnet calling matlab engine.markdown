---
layout: article
title: opnet调用matlab引擎
date: 2017-01-03 18:40:46 +0800
categories: 工具
tag: opnet
---

* content
{:toc}

**环境：**  

<!-- more -->
`matlab2014b (win32) + opnet14.5 （32位）+ vs2010 + win10`

**环境变量设置：**

> **include:**  
>  G:\VS2010\VC\include  
>  C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\Include  
>  G:\opnet\opnetinstall\14.5.A\sys\include  
>  G:\opnet\opnetinstall\14.5.A\models\std\include  
>  **G:\matlab2014b\extern\include**
>
> **lib:**  
>  G:\VS2010\VC\lib  
>  C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\Lib  
>  G:\opnet\opnetinstall\14.5.A\sys\lib  
>  G:\opnet\opnetinstall\14.5.A\sys\pc_intel_win32\lib  
>  **G:\matlab2014b\extern\lib\win32\microsoft**
>
> **path:**  
>  G:\VS2010\VC\bin  
>  G:\VS2010\Common7\IDE  
>  G:\VS2010\Common7\Tools  
>  G:\opnet\opnetinstall\14.5.A\sys\pc_intel_win32\bin  
>  **G:\matlab2014b\bin\win32**

（以上根据自己的安装路径进行修改）

**注意：**  
在已安装opnet和vs的基础上，下载matlab（注意与你的opnet版本要相合，我之前电脑中已安装win64位的matlab，但我的opnet运行的是32位的，所以报错，后来又重新安装了32位版本才没有问题）。加粗部分是安装了matlab之后需要添加的环境变量。需要特别注意的是，在matlab安装之后，点击查看环境变量path，会看到系统会自动给你添加了G:\matlab2014b\bin，一定要再在后面加上\win32，因为系统搜索的时候不会搜索子文件夹里面文件，而很多必需文件是在win32子文件夹里的，所以切记切记。

接着修改opnet的prefrence中的一些参数：(编译和运行)

>   * comp_flags_common：添加 `/IG:\matlab2014b\extern\include`
> （注意格式`/I+matlab库文件目录`）
>   * bind_shobj_flag：添加
> `“/libpath:”G:\matlab2014b\extern\lib\win32\microsoft”`
> （格式`/libpath:matlab库文件目录`）
>   * bind_shobj_libs：添加 `libmx.lib libmat.lib libeng.lib`
>

然后就可以在opnet的进程域中编写代码，通过调用matlab引擎来实现和matlab联合仿真，具体的编程可以参考matlab引擎函数的使用。注意，需要在HB中声明`#include
"engine.h"` 。

