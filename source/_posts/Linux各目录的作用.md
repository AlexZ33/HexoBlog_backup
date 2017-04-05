---
title: Linux 各目录的作用  
date: 2016-0-30 13:44:12
tags:
- 后端
- 笔记
- linux
categories:  linux
---


/根目录
![](http://on891bjlf.bkt.clouddn.com/linux/640.png)

/bin

bin是binary的缩写。这个目录沿袭了UNIX系统的结构，存放着使用者最经常使用的命令。例如cp、ls、cat，等等。命令保存目录（普通用户就可以读取的命令）
  根目录下的bin和sbin，usr目录下的bin和sbin，这四个目录都是用来保存系统命令的。
  其中，bin目录下的命令任何用户都可以执行，sbin目录下只有root才可以执行。
  linux使用此方式来区分用户权限。
![](http://on891bjlf.bkt.clouddn.com/linux/640%20%281%29.png)
![](http://on891bjlf.bkt.clouddn.com/linux/640.jpg)

/boot
启动目录，启动相关文件，这里存放的是启动Linux时使用的一些核心文件。
![](http://on891bjlf.bkt.clouddn.com/linux/640%20%281%29.jpg)

/dev
设备文件保存目录
dev是device（设备）的缩写。这个目录下是所有Linux的外部设备，其功能类似DOS下的.sys和Win下的.vxd。在Linux中设备和文件是用同种方法访问的。例如：/dev/hda代表第一个物理IDE硬盘。
![](http://on891bjlf.bkt.clouddn.com/640%20%282%29.jpg)
/etc
配置文件保存目录这个目录用来存放系统管理所需要的配置文件和子目录。
![](http://on891bjlf.bkt.clouddn.com/linux/640%20%283%29.jpg)
/home
普通用户的家目录
用户的主目录，比如说有个用户叫zk，那他的主目录就是/home/zk也可以用~zk表示。
![](http://on891bjlf.bkt.clouddn.com/linux/3432.png)
![](http://on891bjlf.bkt.clouddn.com/linux/640%20%283%29.png)

/lib
系统库保存目录
这个目录里存放着系统最基本的动态链接共享库，其作用类似于Windows里的.dll文件。几乎所有的应用程序都须要用到这些共享库。


![](http://on891bjlf.bkt.clouddn.com/linux/1.png)
/mnt
系统挂载目录
这个目录是空的，系统提供这个目录是让用户临时挂载别的文件系统。
![](http://on891bjlf.bkt.clouddn.com/linux/2.png)
/media
挂载目录

/root
超级用户的家目录
系统管理员（也叫超级用户）的主目录。作为系统的拥有者，总要有些特权啊！比如单独拥有一个目录。

![](http://on891bjlf.bkt.clouddn.com/linux/3.png)
/tmp
临时目录
这个目录不用说，一定是用来存放一些临时文件的地方了。

/sbin
命令保存目录（超级用户才能使用的目录）
s就是Super User的意思，也就是说这里存放的是系统管理员使用的管理程序。


/proc
直接写入内存（是内存中有关系统进程的实时信息）这个目录是一个虚拟的目录，它是系统内存的映射，我们可以通过直接访问这个目录来获取系统信息。也就是说，这个目录的内容不在硬盘上而是在内存里。

/sys
直接写入内存（是有关系统内核以及驱动的实时信息）
这个目录中存放着那些不断在扩充着的东西，为了保持/usr的相对稳定，那些经常被修改的目录可以放在这个目录下，实际上许多系统管理员都是这样干的。顺带说一下系统的日志文件就在/var/log目录中。 
![](http://on891bjlf.bkt.clouddn.com/linux/4.png)

  porc同sys目录不能直接操作，这两个目录保存的是内存的挂载点。
  其中的数据直接写在内存中。避免数据丢失或由于内存溢出导致系统崩溃。

/usr系统软件资源目录
这是最庞大的目录，我们要用到的应用程序和文件几乎都存放在这个目录下。其中包含以下子目录：
![](http://on891bjlf.bkt.clouddn.com/linux/5.png)

/usr/bin
存放着许多应用程序；
系统命令（普通用户）

/usr/sbin
给超级用户使用的一些管理程序就放在这里；
系统命令（超级用户）

/usr/include
Linux下开发和编译应用程序需要的头文件，在这里查找；

/usr/lib
存放一些常用的动态链接共享库和静态档案库；

/usr/local
这是提供给一般用户的/usr目录，在这里安装软件最适合；

/usr/src
Linux开放的源代码就存在这个目录，爱好者们别放过哦！

/var
系统相关文档内容
这个目录中存放着那些不断在扩充着的东西，为了保持/usr的相对稳定，那些经常被修改的目录可以放在这个目录下，实际上许多系统管理员都是这样干的。顺带说一下系统的日志文件就在/var/log目录中。