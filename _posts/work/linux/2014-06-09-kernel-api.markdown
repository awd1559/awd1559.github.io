---
layout:     post
title:      "api"
subtitle:   " \"kernel api\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - linux kernel
---
部分内容属于2.6

1、进程管理
set_task_state(task, state);		//设置任务状态
	set_current_state(state);

for_each_process(task)	//遍历任务队列
next_task(task)
prev_task(task)

kernel_thread();	//创建内核线程


2、进程调度
set_tsk_need_resched();		//set task->need_resched
clear_tsk_need_resched();	//clear task->need_resched
need_resched();			//判断


3、系统调用
4、中断
request_irq()		//注册总段处理程序
free_irq()		//

local_irq_disable();	//
local_irq_enable();	//

unsigned long flags;
local_irq_save(flags);	//禁止中断
... ...
local_irq_restore(flags);	//中断恢复到原状态


disable_irq(irq);		//禁止控制器上指定的中短线，等待当前中断完成
disable_irq_nosync(irq);	//不等待当前中断完成
enable_irq(irq);		//
synchronize_irq(irq);		//等待特定的中断处理程序退出

irqs_disabled();		//特定中断线是否禁止
in_interrupt();			//是否处于中断上下文
in_irq()			//内核确实正在执行中断处理程序


5、下半部
struct softirq_action
{
	void	(*action)(struct softirq_action *);
	void	*data;
};


struct tasklet_struct
{
	struct tasklet_struct *next;
	unsigned long state;
	atomic_t count;
	void (*func)(unsigned long);
	unsigned long data;
};








6、内核同步
7、定时
8、内存管理
struct page* alloc_page();		//分配一页
struct page* alloc_pages();		//分配多页

unsigned long __get_free_page		//分配一页
unsigned long __get_free_pages		//分配多页

__free_pages(struct page* page, order);
free_page(unsigned long addr);
free_pages(unsigned long addr, order);


void* page_address(struct page* page);	//逻辑地址

void * kmalloc (size_t size, int flags);	//分配指定大小的内存,从size-N的slab中获得内存
void kfree (const void *objp);


void * vmalloc (unsigned long size);		//分配虚拟地址连续的内存
void vfree(void * addr);


slab
--------------------------------------
kmem_cache_t* kmem_cache_create();				//创建高速缓冲
int kmem_cache_destroy (kmem_cache_t * cachep);			//销毁
void * kmem_cache_alloc (kmem_cache_t *cachep, int flags);	//使用
kmem_cache_free();


高端内存映射
--------------------------------------
kmap		//永久映射
kunmap
kmap_atomic	//临时映射
kunmap_atomic




9、虚拟文件





10、块IO



11、进程地址空间
12、页高速缓存
13、模块
14、kobject sysfs