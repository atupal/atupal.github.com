---
layout: post
title: "Execute remote X client on Secure Shell for chrome in Win7"
date: 2013-03-15 14:14
comments: true
categories: 
---

##1.use putty
### download putty:
http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
可以下载一个zip,里面包含了网页列表上的工具,不过我们只需要putyy.exe就够了.
### download xming:
http://xming.en.softonic.com/download
xming是一个运行在windows上的X server. 在这里,我们的linux主机上的gui程序就相当于
x client, 要让远程的linux主机上的gui程序运行在windows上就必须在windows主机上装上
一个 x server, xming是一个开源的免费软件, 够使用了
###config xming:
装完xming之后在开始菜单便会多出xming,xlaunch等,点击启动启动xlaunch,然后全部按默认
的配置设置好.
###config putty:
putty的配置比较简单,只需配置一下ssh里的X11项,选中enable X forwading
X server地址填:localhost:0
协议选中Mit-cookie-啥啥的.
然后打开putty,如果此时出现error:can not open DISPAY:localhost:0时.可以点击xming的托盘
然后查看log,如果有reject 啥啥的就先推出xming.右键开始菜单的xming,然后在启动参数里加上-ac
以特权模式运行就可以了,点击xming启动X server 即可.
ps:记得在linux(client)在/etc/sshd/sshd.conf的文件里打开Xforward yes,默认是关闭的.

##2. use Secure shell for chrome:
这个没有用到ssh转发,因为一直不成功,不知道是不是Secure shell 的问题.
这个直接利用X 协议就行,不过不是很安全.
打开xming,然后ssh到linux client后直接export DISPLAY=你的X server IP地址:0就行了,
或者直接设置你的ssh配置文件或者.bashrc文件
