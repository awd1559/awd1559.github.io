---
layout:     post
title:      "io"
subtitle:   " \"Linux IO Porgram\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - linux prog
---
//文件IO
===============================================
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
int open(const char* pathname, int oflag, .../*, mode_t mods */);	//返回文件描述符
	oflag
	O_RDONLY	0	只读
	O_WRONLY	1	只写
	O_RDWR		2	读写
	O_APPEND		写到文件尾
	O_CREAT			若不存在则创建，需要创建mods
	O_EXCL			同时指定O_CREAT， 文件存在则出错，文件不存在则创建
	O_TRUNC			若文件存在，且只读或只写打开，则文件长度截短为0
	O_NOCTTY		若打开终端设备，则不将此设备分配为此进程的控制终端
	O_NONBLOCK		若打开FIFO、块文件、字符文件，为此文件的本次打开操作和后续的IO操作设置非阻塞方式
	O_SYNC			每次write都等到物理IO完成才返回，同步


===============================================
#include <sys/types.h>
#include <sys/stat.h>
#icnlude <fcntl.h>

int creat(const char* pathname, mode_t mode);		//返回文件描述符
open(pathname, O_WRONLY|O_CREAT|O_TRUNC, mode);		//等价于


===============================================
#include <unistd.h>
int close(int filedes);		//成功:0, 出错:-1

===============================================
#include <sys/types.h>
#include <unistd.h>

off_t lseek(int filedes, off_t offset, int whence);		//如果文件为管道文件或FIFO，返回-1
//whence
//SEEK_SET	设置文件当前位置为 文件开始+offset，offset取正值
//SEEK_CUR	设置文件当前位置为 当前位置+offset，offset取正负值
//SEEK_END	设置文件当前位置为 文件长度+offset，offset取正负值

off_t currpos = lseek(fd, 0, SEEK_CUR);		//获取文件当前位置
//如果文件为管道文件或FIFO，返回-1
//lseek不引起文件IO
//文件位移可以大于文件长度，对该文件的下一次写将延长文件，并留下空洞


===============================================
#include <unistd.h>
ssize_t read(int filedes, void *buff,  size_t nbytes);		//返回读到的字节数，0为文件尾

//从终端设备读时，一次最多读一行
//从网络读时，最多读取缓冲中的字符数

#include <unistd.h>
ssize_t write(int filedes, const void* buff, size_t nbytes);	//返回已写的字节数


===============================================
#include <unistd.h>
int dup(int filedes);	//返回当前最小的可用文件描述符
			//等效于fcntl(filedes, F_DUPFD, 0);
int dup2(int filedes, int filedes2);		//已filedes2指定新描述符的数值, 如果filedes2已经打开，先将其关闭
			//等效于close(filedes2); fcntl(filedes, F_DUPFD, filedes2);



#include <sys/types.h>
#include <unistd.h>
#include <fcntl.h>

int fcntl(int filedes, int cmd, ... /* int arg */);	
	cmd
	F_DUPFD		//复制现存的描述符， 		返回新文件描述符
	F_GETFD		//获得/设置文件描述符标志	返回文件描述符标志
	F_SETFD		
	F_GETFL		//获得/设置文件状态标志		
	F_SETFL		
	F_GETOWN	//获得/设置异步I/O有权
	F_SETOWN
	F_GETLK		//获得/设置记录锁
	F_SETLK
	F_SETLKW
	

	F_GETFL/F_SETFL
	文件状态标志位
	O_RDONLY	//只读打开
	O_WRONLY	//只写打开
	O_RDWR		//读写打开,	这三个的掩码为O_ACCMODE
	O_APPEND	//写时添加至文件尾
	O_NONBLOCK	//非阻塞方式
	O_YNC		//等待写完成
	O_ASYNC		//异步IO



======================================================================================
#include <unistd.h>
#include <sys/ioctl.h>

int ioctl(int filedes, int request, ...);	




======================================================================================

