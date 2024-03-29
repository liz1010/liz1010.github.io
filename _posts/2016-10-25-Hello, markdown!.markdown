---
layout: article
title: Hello，Markdown！
date: 2016-10-25 14:49:13 +0800
categories: 工具
tag: markdown
---

* content
{:toc}

* * *

<!-- more -->

### **前言**

打算写博客的我，发现从简书到CSDN，这两者都提供Markdown编辑器，甚至比起传统的富文本编辑器，它们鼓励使用Markdown编辑器。另外，一些我关注的博主也十分推荐使用Markdown语法写文章，Markdown这个词出现得越发频繁，到底什么是Markdown，Markdown的魅力何在？在好奇心的驱使下，我查找了一些资料，进行了如下总结。

* * *

### **什么是Markdown？**

Markdown是一种轻量级的标记语言，所谓标记语言就是将文本以及与文本相关的其他信息结合起来，展现出关于文档结构和数据处理细节的电脑文字编码，这些其他信息采用标记进行标识。而轻量级是相对于如HTML等相对复杂的标记语言而言，因为Markdown的语法很简单，常用的标记符号不超过十个。Markdown的目标是实现“易读易写“，Markdown语法的目标是成为一种适用于网络的书写语言，它兼容HTML。  
详细的文档说明可参看：[Markdown语法说明](http://wowubuntu.com/markdown/#autoescape)

* * *

### **为什么要用Markdown进行写作？**

  * 使用方便   

    * 语法简洁明了，学习容易，使我们专注于文字内容而不是排版。对于操作熟练的宝宝，基本可以手不离键盘。
    * 格式多样，Markdown导出格式多样，除了本身的.md文件，可另存为HTML、word、Latex、PDF、epub等格式文件输出。
    * 纯文本内容，兼容所有的文本编辑器和字处理软件。
    * 平台支持广，github、reddit、stackoverflow，简书，csdn等。
  * 可读性好   

    * 风格简洁，代码高亮，排版好的文章给人一种优雅的感觉。

* * *

### **Markdown常用语法介绍**

#### 区块元素

  * 段落与换行   
一个Markdown段落有一个或多个连续的文本行组成，它的前后要有一个以上的空行（空行的定义是看起来像是空的，便会被视为空行，比方说，若是一行只包含空格和制表符，则该行也会被视为空行。普通段落不该用空格或制表符来缩进。

这是官方解释，我感觉有点晦涩，我的理解是分段就是输完这一段的最后一句，连续两次enter再输入下一段，如果想要保持中文中段落首句缩进的格式，可以先将输入法改为全角，再输入两个空格。

如何输入空行？如前所述，因为Markdown兼容HTML，所以可以直接输入<br/>，或者输入`&ensp;`，注意分号不能丢。

![这里写图片描述](/images/你好,减价!_1.png)

  * 特殊字符自动转换   
在HTML文件中有两个字符需要特殊处理：`<`和`&`。分别用`&lt;` `&amp;`来代替。

  * 标题（类atx形式）   
# 一级标题  
## 二级标题  
### 三级标题  
以此类推总共六级标题

![这里写图片描述](/images/你好,减价!_2.png)

  * 区块引用blockquotes   
在整个段落的第一行情最前面加上>，或者在每行的最前面加上>  
引用的区块内可以再叠用其他的markdown语法，包括标题，列表，代码区块等。

![这里写图片描述](/images/你好,减价!_3.png)

  * 分割线   
在一行中用三个以上的星号，底线或减号来建立一个分隔线，行内不能有其他东西，也可以在星号或减号中间插入空格。

  * 列表   
分为有序列表和无序列表，无序列表的表示只需要在文字前加上`-`或 `*`，与有序列表则直接在文字前加`1.` `2.`
`3.`，注意`-`，`*`以及序号与文字之间均需加上空格。

![这里写图片描述](/images/你好,减价!_4.png)

  * 代码区块   
建立代码区块很简单，只需要简单的缩进4个空格或一个制表符(tab)，或者将` ` `置于这段代码的首行和末行

## 区段元素

  * 强调   
使用星号 _和底线_作为标记强调字词的符号，用两个_ 包含一段文本是粗体，用一个_包含是斜体。

  * 代码   
如果要标记一小段行内代码，可以用反引号把它包起来（`）

  * 公式   
$$公式$$

![这里写图片描述](/images/你好,减价!_5.png)

  * 图片   
插入连接与插入图片的语法很像，区别在一个！号  
图片为:！[ ](){ImgCap}{/ImgCap}  
链接为: [ ]( )

这里，我要插入Markdown语法的官方文档:[Markdown语法说明（简体中文版）](http://www.appinn.com/markdown/)

  * 反斜杠

    
    
        \
        `
        *
        _
        {}
        []
        ()
        #
        +
        _
        ·
        ！

* 换行
  两个空格

* 空行
  `<br>`

* * *

我觉得只需先记忆一些最简单常用的语法，就可以开始使用Markdown编辑器。Markdown的所写即所见，可以很方便的帮助记忆，更复杂高级的用法根据以后的日常学习需求慢慢熟练即可。

起先我下载了马克飞象的Markdown编辑器，可是发现马克飞象需要收费而且并不便宜，然后下载了作业部落的cmd
Markdown，不过我发现，这两个客户端版的Markdown编辑器都不支持复制粘贴，我想把Onenote写好的部分内容复制粘贴到里面，可是不行！还好CSDN支持┗|｀O′|┛
嗷~~

总之，这只是一篇关于Markdown的初级介绍，等日后熟练，希望能分享一篇更加详尽复杂的Markdown使用总结与大家探讨交流嘿嘿。

