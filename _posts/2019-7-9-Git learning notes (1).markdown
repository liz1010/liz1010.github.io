---
layout: article
title: Git学习笔记-基础1
date: 2019-07-09 15:49:12 +0800
categories: Git
tag: Git
---

* content
{:toc}



## 概述

Git是一种分布式版本控制系统，在分布式版本控制系统中，客户端并不只提取最新版本的文件快照，而是将整个代码仓库完整的镜像下来。

## Git的特点

直接记录快照，而非差异比较

近乎所有操作都是本地执行

基于计算校验和保证数据完整性

## Git的四个工作区域

工作目录（workbench）：自己电脑中能看到的目录

暂存区（stage/index）：一般存放在.git目录下的index文件（.git/index），所有暂存区有时候也叫索引

版本库（repository）：Git的版本库.git, 用来保存项目的元数据和对象数据库的地方，是Git中最重要的部分

远程仓库（remote directory）：远程仓库，托管代码的服务器

![](https://img-blog.csdnimg.cn/20190709155928130.png?x-oss-
process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTIzNDg2OTI=,size_16,color_FFFFFF,t_70)

![](https://img-blog.csdnimg.cn/20190709154820432.png?x-oss-
process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTIzNDg2OTI=,size_16,color_FFFFFF,t_70)

## Git文件的几种状态

未跟踪（untracked）：此文件在文件夹中，但没有加入到git库，不参与版本控制，通过git add状态变为staged

未修改（unmodify）：文件已经入库，未修改，如果使用git rm 移出版本库，则成为untracked文件

已修改（modified）：修改了文件，但还没保存在数据库中，通过git add进入暂存状态，使用git
checkout则丢弃修改，返回到unmodify状态

已暂存（staged）：对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中，执行git
commit则同步到库中，这是库中的文件和本地文件又变为一致，未见为unmodify状态

已提交（committed）：数据已经安全保存在本地数据库中

![](https://img-blog.csdnimg.cn/2019070915483142.png?x-oss-
process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTIzNDg2OTI=,size_16,color_FFFFFF,t_70)

## git常用指令

Git config --list 给出所有配置指令

Git init 在现有目录中初始化仓库

Git clone 【url】 文件夹名 克隆现有仓库

Git status 查看当前文件状态（-s 状态简览）为暂存和已经暂存

Git add file 跟踪新文件，以及暂存新的修改

Git diff 显示尚未暂存的改动

Git commit -m "提交信息" 提交更新

Git commit -a 跳过使用暂存区域，即git会自动把所有已经跟踪过的文件暂存起来一并提交。

Git rm file 移除文件（从暂存区删除），该文件不再纳入版本管理

Git mv file_from file_to 移动文件

Git log 显示提交历史

Git remote -v 显示所有的远程仓库（-v会现实需要读写远程仓库使用的git保存的简写及其对应的URL）

Git fetch 【remote-name】

Git push origin master 推送到远程仓库

Git config --global alias.co checkout 给checkout取别名为co

## Ref
<https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%85%B3%E4%BA%8E%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6>

