---
layout:     post
title:      "slab"
subtitle:   " \"linux kernel mm slab\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - linux kernel
---
slab
===============================================================
将内核中经常使用的对象放在告诉缓存中，保持对象在初始的状态
所有对象由kmem_cache_s管理

全局struct kmem_cache_t cache_cache
kmem_cache_s
{
	... ...
	struct list_head slabs_full;				//slab_t放入三个列表中的一个
	struct list_head slabs_partial;
	struct list_head slabs_free;
	void (*ctor)(void *, kmem_cache_t *, unsigned long);	//对象的构造函数
	void (*dtor)(void *, kmem_cache_t *, unsigned long);	//对象的析构函数
	char   name[CACHE_NAMELEN];				//高速缓存的名字
	struct list_head	next;				//在cache_cache中的连接

	unsigned int objsize;			//slab中对象的大小
	unsigned int num;			//每个slab中包含的对象个数
	... ...
}



kmem_cache_create(name, size, offset, flag, ctor, dtor)		
				//创建命名的对象集,从slab的offset开始存放起
				//每个对象的大小
				//用ctor函数初始化对象
				//用dtor函数销毁使用过的对象
	-kmem_cache_alloc	//从cache_cache中分配一个keme_cache_s
	-kmem_cache_estimate	//计算对象数量
		保存(slab_t, n*(object + kmem_bufctl_t)

kmem_cache_free			//释放对象，返回给高速缓存
kmalloc					//寻找满足所需内存大小的高速缓存，从中存分配一块内存
kfree					//释放kmalloc分配的内存


slab描述符
slab_s
{
	... ...
	struct list_head list;	//放入kmem_cache_t的slabs_full, slabs_free,slabs_partial队列中的一个
	void *s_mem;			//slab中第一个对象的起始地址
	kmem_bufctl_t free;		//bufctls数组,存储空闲对象的位置
}




系统维护两个由小内存缓冲区所构成的高速缓存集



