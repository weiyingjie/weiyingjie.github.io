---
title: APUE-UNIX基础知识
date: 2020-08-04 00:20:32
---

![知识脑图](https://cdn.jsdelivr.net/gh/Creeper-boom/cdn/img/markdown/UNIX基础知识.png)

## GNU/Linux系统
&emsp;&emsp;我们常说的Linux系统其实是GNU/Linux系统，GNU（GNU’s Not Unix）系统是一个类Unix操作系统，但是这个操作系统自成立以来到现在依然没有完善，它是一个完全自由的操作系统，遵循着自由软件哲学理念。
&emsp;&emsp;到90年代初，GNU操作系统初具雏形，它拥有了除内核外操作系统所应该具备的一切，并且在1990年开始开发自己的内核GNU Hurd。但是内核的开发工作并不顺利。而在1991年，Linus Torvalds基于GPL协议（GNU通用公共许可证）发布了类Unix的内核Linux，并且一经发布就广受好评，但是这也仅仅是一个内核。
&emsp;&emsp;这时GNU已经完善到只有内核，而Linux只有内核，所以两个“开源大佬”也就进行了结合，并进行了诸多完善，最终形成了GNU/Linux系统，也就是我们现在简称的Linux系统。而我们常用的gcc(GNU Compiler Collection)是GNU的编译组件，包含了很多常用语言及各自的库。

## shell
shell是一个命令解释器，用户可以通过shell进行一些输入、执行命令等等。

	/etc/passwd中每个用户的最后一个字段为登录shell

| 名称               | 路径      | FreeBSD 8.0 | Linux 3.2.0 | Mac OS X 10.6.8 | Solaris 10 |
| ------------------ | --------- | ----------- | ----------- | --------------- | ---------- |
| Bourne shell       | /bin/sh   | -           | -           | bash的副本      | -          |
| Bourne-again shell | /bin/bash | 可选的      | -           | -               | -          |
| C shell            | /bin/csh  | 链接至tcsh  | 可选的      | 链接至tcsh      | -          |
| Korn shell         | /bin/ksh  | 可选的      | 可选的      | -               | -          |
| TENEX C shell      | /bin/tcsh | -           | 可选的      | -               | -          |

==其中Bourne-again shell (即BASH) 是GNU shell，所有Linux系统都提供这种shell==

## 文件和目录

### 文件
==Linux中**一切皆文件**== 
&emsp;&emsp;在Linux中，所有的东西都是一个文件。如显示设备（显示器），即为一个文件，可以对其进行读写操作进而完成相应的显示；输入设备（如键盘）也是一个文件，读取该文件的内容即可完成输入。


### 文件系统
&emsp;&emsp;文件系统是目录和文件的层次结构，起点为" / " 根目录

### 目录
&emsp;&emsp;目录为一个包含目录项的文件，可以类比Windows下的”文件夹“概念。

### 路径
- 绝对路径：从 / 开始，如`/etc/passwd`
- 相对路径：相对于当前位置的路径，" . 和 .." 分别表示当前目录和上级目录，如想表示上级目录中的test.txt，则为`../test.txt`

## 输入输出

### 文件描述符
&emsp;&emsp;文件描述符通常为非负整数，用于标识特定进程正在访问的文件。内核打开或创建一个文件是都会返回一个文件描述符。通过文件描述符可以进行读写操作

### 标准输入、标准输出和标准错误
&emsp;&emsp;通常情况，每运行一个新程序时，shell都打开3个文件描述符
- 标准输入(stdin)为0
- 标准输出(stdout)为1
- 标准错误(stderr)为2

## 程序和进程

### 程序
&emsp;&emsp;程序是一个可执行文件，内核使用exec函数将程序读入内存并执行

### 进程
&emsp;&emsp;程序的执行实例为进程，每一个进程都有唯一标识，称为进程ID（非负整数）
进程主要通过 fork(), exec(), waitpid()函数进行控制

### 线程
&emsp;&emsp;通常一个进程只有一个控制线程。一个进程内所有线程共享同一地址空间、文件描述符、栈等等。正因为如此，多个进程对于同一内容进行操作时要进行进程同步的控制。

## 出错处理

&emsp;&emsp;当UNIX系统函数出错时，通常返回负值（也有返回NULL等等），errno通常被设置为有特定信息的值。在打印出错信息时，可选：
- `char *strerror(int errnum);`
- `void perror(const char *msg);`

## 用户标识

### 用户ID
&emsp;&emsp;不同用户有自己的用户ID进行标识及权限管理，其中超级用户root的UID为0

### 组ID
&emsp;&emsp;可以通过组ID进行权限控制

## 信号
&emsp;&emsp;信号用于通知进程发生了某种情况，在键盘上有两种产生信号的方法：
- 中断键(Ctrl + D)
- 退出键(Ctrl + \)

另一种产生信号的方式为调用kill()函数