---
layout:     post
title:      "page cache"
subtitle:   " \"page cache\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - linux kernel
---
页面高速缓存(page cache)
================================================================
所有页面都放到一个hashtable中: page_hash_table,2.6不再使用这种管理方式,而是通过基树检索
page->next_hash, page->pprev_hash处理hash冲突


address_space
{
	sruct inode *host;		//如果非null，该高速缓存与inode相关，否则swapper关联
	... ...
	struct list_head clean_pages;	//这个队列中的页面均与inode相关
	struct list_head dirty_pages;	//
	struct list_head locked_pages;	//page通过page->list加入这三个队列
	struct address_space_oprations *a_ops; 
	... ...
}
add_to_page_cache()      //将page加入address_space->clean_pages
	-add_page_to_inode_queue()

页面高速缓存(page cache)：预读磁盘数据到页面，暂时保留长期不用的页面
页面高速缓存对象:addresss_space
这些缓存的页面对应于普通文件、块设备、交换分区


page LRU list
==============================================================
mm/page_alloc.c中定义两个全局变量:inactive_list, active_list
页面通过page->lru在这两个list中保存
refill_inactive() 	//将页面从active_list尾部移动到inactive_list中，保证active_list中页面数量是inactive_list中页
面数量的2/3





系统中所有正在使用的页面都存放在页面高速缓存中? page->lru
mark_page_accessed(page)
	-active_page(page)
		-add_page_to_active_list()  //将page->lru加入全局active_list队列中
