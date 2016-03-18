---
layout:     post
title:      "kernel asm script"
subtitle:   " \"kernel asm script\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - linux kernel
---
switch_to

从终端或异常处理程序返回，如果当前内核控制路径只有一个，则返回用户态
如果有其他的请求，则继续执行请求
如果没有请求，处理当前进程未处理的信号，并代表当前进程继续在内核态执行
ret_from_intr			//终止中断处理程序
	//在ebx中装入当前进程描述符的地址,ret_from_sys_call要求
	//ret_from_exception
	
ret_from_exception		//终止除0x80异常外的所有异常
	//从cs和eflags寄存器中判断是否运行在用户态
	//如果在内核态, ret_from_sys_call
	//否则被中断的内核控制路径重新开始
	
ret_from_sys_call		//ebx中是current的地址
	//检查need_resched
	jne reschedule		//需要调度
	cmpl $0, 8(%ebx) 	//检查sigpending字段
	jne signal_return
	jmp restore_all		//如果无未处理信号,恢复硬件环境
	
reschedule:
	call schedule
	jmp ret_from_sys_call
	

signal_return:
	
ret_from_fork			//

