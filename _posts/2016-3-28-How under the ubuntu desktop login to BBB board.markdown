---
layout: article
title: 如何在ubuntu下桌面登录到BBB板
date: 2016-03-28 10:35:34 +0800
categories: Linux
tag: Linux
---

* content
{:toc}

因为实验需求,需要在俩个BBB板之间建立通信.为方便实验,需要每个板开启多个终端,可是pc通过串口线登入BBB板只有一个终端,由此求诸于进入bbb桌面,开启多个终端.

<!-- more -->

经过资料收集及实践,步骤如下:

**准备:**

一台PC(ubuntu系统),一个BBB板

**步骤:**

将BBB通过网线连接到pc所在路由器上,两者可ping通,BBB串口插到pc上.

  

- BBB:(服务端)  

1.由于BBB安装系统为debian7.4(查看版本:lsb_release
-a),默认安装VNC软件,所以直接执行vncserver命令,按提示配置下密码.注:如果忘记密码或者要更改密码,可通过命令vncpasswd进行重置.

2.给当前用户设置vnc登录密码:$ vncpasswd

3.修改vnc默认设置,使启动时运行gnome作为X的桌面:

$ vncserver :1

$ vncserver: -kill 1  

注意：里面的":1"代表display号，客户登录的时候得写相同的display号才能登录。

4.修改~/.vnc/xstartup文件，建议拷贝系统中Xsession的配置文件：

$ cp /etc/X11/Xsession ~/.vnc/xstartup

$ cp /etc/X11/Xsession ~/.vnc/xstartup

5.再次启动VNC SERVER：

$ vncserver -geometry 1280x800 :1

$ vncserver -geometry 1280x800 :1

  

- PC:(客户端)

1.在ubuntu操作系统下下载vncviwer软件包:sudo apt-get install xvnc4viewer

2.远程登录BBB板:$ vncviwer IP(BBB):1

  

OK!  

  

  

