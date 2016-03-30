---
layout:     post
title:      "bootmem"
subtitle:   " \"bootmem\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - linux kernel
---
引导内存分配器			//setup_arch,检测内存分布，初始化内存分配位图
-----------------------------------------------
每一个节点有一个bootmem_data,包含已分配页面的位图等
struct bootmem_data
{
	unsigned long node_boot_start;	//起始物理地址
	unsigned long node_low_pfn;	//结束地址
	void *node_bootmem_map;		//已分配页面和空闲页面的位图
	unsigned long last_offset;	//最后一次分配所在页面的偏移
	unsigned long last_pos;		//最后一次分配是的页面帧
}

mem_init		//销毁引导内存分配器的数据


物理内存分配
伙伴算法管理空闲块
struct free_area_t
{
	struct list_head	free_list;	//head of page->list
	unsigned long		*map;		//表示伙伴状态的位图
}







虚拟内存块描述符
struct vm_struct
{
	unsigned long flags;
	void * addr;			//块的起始地址
	unsigned long size;		//块的大小
	struct vm_struct * next;
}

全局变量
struct vm_struct * vmlist;
get_vm_area()			//线性查找vmlist列表

vmalloc()		//在连续的虚拟地址空间分配内存
	get_vm_area
vmalloc_dma()		//
vmalloc_32()		//
