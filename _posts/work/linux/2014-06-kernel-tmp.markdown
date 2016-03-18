---
layout:     post
title:      "kernel"
subtitle:   " \"tmp note\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - linux kernel
---
list_head寄宿在其他宿主数据结构中
INIT_LIST_HEAD(ptr)初始化list_head

举例说明
=================================================
typedef struct page
{
	struct list_head list;  	//page结构可以在这个队列中
	struct list_head lru;		//page结构也可以在这个队列中
	struct page* hash_next;		//hash队列
}


list_add(struct list_head *new, struct list_head *head);
list_del(struct list_head *entry);

list_entry(ptr, type, member);	//获得宿主结构的指针


内核最大可以访问896M(MAXMEM)MAXMAM_PFN


_end是内核映像的结束处，pfn为start_pfn

start_kernel
	-setup_arch
		调用e820map,获得所有内存地址图
		计算pfn，只有RAM可计算pfn
		init_bootmem(start_pfn, max_low_pfn)
			在start_pfn(_end)， 构建位图，记录所有的pfn，哪些是空洞，哪些不能动态分配
		paging_init()
			pagetable_init    	//扩充asm建立的页表，使用swapper_pg_dir做页目录表
			flush_tbl_all		//将高速缓存的内容刷到内存
			kmap_init			//内核中设置ige全局的pte_t指针kmap_pte,执行页面映射表中的一个表项，这个表项将动态地映射到不同的物理页面
								//每当要访问一个属于“高内存”的物理页面时，
								//就要先改变这个表项。
								//函数kmap_init的作用主要就是设置指针kmap_pte
			frea_area_init
			men_init			
				free_all_bootmem//bootmem位图中的数据不再需要
			






cpu_initialized全局位图，每个CPU在这个位图中都有对应的标志位

资源request_resource
两棵树
iomem_resource
ioport_resource

一个数组
rom_resources[] 
	System ROM (BIOS) 0xF0000~0xFFFFF
	Video ROM	  0xC0000~0xC7FFF


page_cache_init分配空间建立起缓冲页面hash表page_hash_table
以cpu编号为下标的数组init_tasks[]





