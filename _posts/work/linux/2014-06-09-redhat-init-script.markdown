---
layout:     post
title:      "redhat init script"
subtitle:   " \"redhat启动脚本\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - linux kernel
---

redhat启动脚本顺序
加载内核
执行init程序
/etc/rc.d/rc.sysinit
			#调入keymap及系统字体
			#启动swapping
			#设置主机名
			#设置NIS域名
			#fsck 并mount文件系统
			#打开quota
			#装载声卡模块
			#设置系统时钟
/etc/rc.d/rc $RUNLEVEL	#/etc/inittab中设定$RUNLEVEL
			#执行相应等级目录下的脚本/etc/rc.d/rc3.d/Sxxx
/etc/rc.d/rc.local
/sbin/mingetty		#等待用户登录
