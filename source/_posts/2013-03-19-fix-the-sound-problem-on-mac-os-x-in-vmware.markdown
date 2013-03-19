---
layout: post
title: "Fix the sound problem on mac os X in vmware"
date: 2013-03-19 13:48
comments: true
categories: 
---

遇到了件比较郁闷的事情，在ArchLinux下的vmware上装了Mac OS 8（顺便说一句，之前一直是在vmware player上配的虚拟机，结果不管我怎么换镜像换darwin.iso
死活都启动不了InstallESD.iso，后来在workstation上面配置了，把cpu改成了单核双线程然后就奇迹般的在vmware player上正常启动了。player
版本是5.0,workstatioin是9.0）。嗯，回到正题，装上后就是没有声音。我的vmware tools和mac os 的声卡驱动程序都已经安装了最新版的。

###vmware sound problem mac
我以这个为关键字然后谷歌到了一篇帖子：http://www.insanelymac.com/forum/topic/276712-snow-leopard-1068-guest-ubuntu-1110-host-vmware-8-no-sound/
最后一个用户说：I got sound working by commenting out the line sound.virtualDev = "hdaudio" from my .vmx file. It's pretty choppy at the moment, but there are several posts about tuning parameters pciSound.DAC2InterruptsPerSec and pciSound.playBuffer. Will try tweaking these now. 
然后我就照着他的做了，重启虚拟机后发现果然有声音了，但是声音是断断续续的。。。大概一秒钟就断一次听起来很不舒服。
该声卡的输入输出频率问题依然没有解决。

###然后继续谷歌“low latency sound vmware mac”
找到下面一篇blog：http://blog.bryansmart.com/2012/02/16/low-latency-sound-for-vmware/
大概是说vmware给虚拟机提供的声卡是自己虚拟出来的，vmware充当物理网卡和虚拟网卡的一个媒介。于是在内存不足的时候vmware可能不能立即响应虚拟机的
数据请求从而造成虚拟机的声音断断续续。怎么解决呢？呵呵，给vmware设置一个soundBuffer就可以了。就是缓存，先一次传输一个缓存大小的数据，然后再输入
这样就不会造成声音断断续续的情况了。但是我照文章中的方法设置了XXX.vmx, 问题依然存在。这个时候我就奇怪了，难道是内存不够大的原因？
但是我已经设置了4G了啊。不管了，然后我直接把内存升到5G。缓存设为400,缓存刷新时间设置为10ms。然后再重启。
OK，声音正常了！
