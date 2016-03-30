---
layout:     post
title:      "swap"
subtitle:   " \"Linux Kernel mm swap\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - linux kernel
---
交换page到交换分区(swap)
=================================================================
当page cache中存在max_mapped个页面(shrink_cache)时，swap_out()被启动，将页面换出。

全局struct mm_struct *swap_mm = &init_mm


alloc_pages->__alloc_pages->balance_classzone
free_more_memory->try_to_free_pages
kswapd->kswapd_balance->kswapd_balance_pgdat
	-try_to_free_pages_zone
		-shrink_caches
			-shrink_cache
				-swap_out

swap_out->swap_out_mm->swap_out_vma
	->swap_out_pgd->swap_out_pmd
	->try_to_swap_out
		-PageSwapCache		//查看页面是否在swap cache中，page->mapping = swapper_space
		-get_swap_page		//获得交换区的一个交换槽
		-add_to_swap_cache	//放入swap cache
		-set_pte		//将交换槽信息写入pte
		

当mm->swap_address=TASK_SIZE，说明该进程已经被完全的搜索了一遍



交换区描述
==============================================================
struct swap_info_struct swap_info[MAX_SWAPFILES];
truct swap_info_struct
{
	... ...
	kdev_t swap_device;		//该交换区所使用的设备
	struct dentry *swap_file;	//交换区挂载的dentry
	struct vfsmount *swap_vfsmnt;
	unsigned short *swap_map;	//交换区中页面槽的位图，槽使用者的引用计数
	... ...
}
多个交换区有优先级，最优先交换区存放在全局变量sturct swap_list_t swap_list,通过swap_into_struct->next在swap_info数组
中寻找

1、每个交换区在磁盘上划出大量页面大小的槽，第一个槽存放交换区信息
2、在页面换出时，相应页表项pte中存放交换槽的信息：交换槽在swap_info中的下标、交换槽在swap_info->swap_map中的偏移量，
   即在pte中存入swp_entry_t
   pte_to_swp_entry()
   swp_entry_to_pte()

   在x86中，
   swp_entry_t的
   第0位:  _PAGE_PRESENT
   1-6位:  标识swap_info数组下标的类型，由宏SWAP_TYPE()返回该值
   第7位:  _PAGE_PROTNONE
   8-31位: 代表交换文件内的页号，即swap_map中的偏移，共24位，交换分区最大2*24*4K=64G, SWAP_OFFSET()返回该值

   SWP_ENTRY(type, offset)，生成一个swp_entry_t

寻找可用的交换槽
get_swap_page()		//从swap_list中的交换区开始寻找可用的交换槽,寻找type
	-scan_swap_map()//寻找在swap_map寻找可用的offset
   
swap_free()		//释放交换槽



交换高速缓存(swap cache)
===============================================================
全局交换高速缓存描述struct swap_cache_info
swap cache总是使用swapper_space作为page->mapping的地址空间
add_to_swap_cache()	//将页面放入swap cache
	-add_to_page_cache_unique	//将page放到page cache




handle_pte_fault->do_swap_page
lookup_swap_cache(entry)	//
read_swap_cache_async		//