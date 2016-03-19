---
layout:     post
title:      "paging"
subtitle:   " \"Linux Kernel paging\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - linux kernel
---
线性地址的格式:
=================================================

|	10位		|	10位		|	12位		|
------------------------------------------------
页目录表index	|	页表index	|	页内偏移	|
------------------------------------------------


cr3:当前进程的页目录表基址

include/asm-i386/page.h
定义
pte_t	//页表项
pmd_t	//页中间表项,用于三层分页
pgd_t 	//页目录表项

pgprot_t//页面保护结构,页表项的低12位

一个page结构代表一个物理页面
所有page保存在mem_map指针链表中

pte_t的前20位就是页的起始物理地址，也是该page结构在mem_map中的索引


=================================================
include/asm-i386/processor.h
在start_thread中卫当前进程指定代码段、数据段、堆栈段，以绕过Intel的段式内存管理 
问：c代码中如何让结构和cpu寄存器相映射

include/asm-i386/segment.h
					index TI RPL
__KERNEL_CS 0x10	00010 0  00		//gdt第2项的索引
__KERNEL_DS 0x18	00011 0  00		//gdt第3项的索引
__USER_CS 0x23		00100 0  11		//gdt第4项的索引
__USER_DS 0x23		00101 0  11		//gdt第5项的索引
数据段和堆栈段是混在一起的

arch/i386/kernel/head.S
初始的GDT内容:
ENTRY(gdt_table)
	B0~B32	基地址全是0
	L0~L19	段的上限全是0xfffff
	G=1	段长单位均为4KB
	D=1	对四个段的访问都是32位指令
	P=1	四个段都在内存
KERNEL_CS、KERNEL_DS的DPL为0
USER_CS、USER_DS的DPL为3
=================================================

_pa()  //内核中根据虚拟地址得到物理地址
如__pa(next-pgd)得到下一进程的页目录表物理地址，放入cr3中

因为内核是从物理地址的0x0000开始的
所以va<=>pa 转化可以通过  -/+ 0xC000 0000(PAGE_OFFSET) 来完成

PAGE_OFFSET		20
PAGE_SHIFT		12
PMD_SHIFT		22
=====================================================


页式存储管理中，如果要将内存换出到硬盘，只要按页交换即可
段式管理，却要整段交换

VM86模式，模拟80286，依然采取段式内存映射
LDT只在VM86模式中使用


在elf格式的可执行文件中，ld总是从0x8000000开始安排程序的"代码段"
========================================================

head.S
========================================================
boot时以pg0、pg1两个页表，代表8M的空间

.org 0x1000
ENTRY(swapper_pg_dir) 	//初始页目录表
						//在用户空间和内核空间分别映射两张页表(pg0, pg1)

.org 0x2000				//初始的两个页表，管理8M空间
ENTRY(pg0)

.org 0x3000
ENTRY(pg1)

ENTRY(empty_zero_page)	//初始化时使用,使用ZERO_PAGE引用
						//也做BIOS和命令行传入的参数暂存地
						//引用参数的地址见PARAM  【arch/i386/kernel/setup.c】
						
						
						

1)开启分页机制
2)以一个符号地址为绝对转移指令，ip即在系统空间取指令

将系统堆栈设在ENTRY(stack_start), 即在swapper (init_task_union)进程描述符的高地址处

========================================================




