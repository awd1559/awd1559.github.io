---
layout:     post
title:      "data struct"
subtitle:   " \"linux kernel data struct\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - linux kernel
---

节点
------------------------------------------------------------
struct pg_data_t {					//NUMA非一致内存访问
	zone_t node_zones[MAX_NR_ZONES];
	zonelist_t node_zonelists[GFP_ZONEMASK+1];
	int nr_zones;
	struct page *node_mem_map;
	unsigned long *valid_addr_bitmap;
	struct bootmem_data *bdata;
	unsigned long node_start_paddr;			//节点的起始物理地址
	unsigned long node_start_mapnr;			// index of start page in mem_map[]
	unsigned long node_size;
	int node_id;
	struct pg_data_t *node_next;			//所有内存节点连在一起,放入pgdat_list
}
全局变量
pg_data_t *pgdat_list;					//对于UMA结构的pc来说，列表中只有一个对象
pg_data_t contig_page_data;



管理区
------------------------------------------------------------
struct zone_t
{
	unsigned long free_pages;
	unsigned long pages_min, pages_low, pages_high;
	int need_balance;
	
	free_area_t	free_area[MAX_ORDER];
	wait_queue_head_t*	wait_table;

	struct pglist_data* 	zone_pgdat;		//指向节点结构
	struct page*		zone_mem_map;		//管理区管理的page在mem_map中第一页的index
	unsigned long 		zone_start_paddr;	//同node_start_paddr
	unsigned long 		zone_start_mapnr;	//同node_start_mapnr
}

空闲页面小于pages_low, 伙伴分配器唤醒kswapd释放页面



页面对象
-----------------------------------------------------
struct page
{
	struct list_head list;		/* ->mapping has some page lists. */
					//用于free_area_t中
					//用于address_space中
	struct address_space *mapping;	//页所属于的address_space
	unsigned long index;		//在mapping中的索引，已页大小为单位
	struct page *next_hash;		//page_hash_table
	struct page **pprev_hash;

	atomic_t count;			//usage count
	struct list_head lru;		//inactive_list or active_list
	struct buffer_head * buffers;	/* Buffer maps us to a disk block. */

}

struct page **page_hash_table; 	//page_hash(宏得到hash槽)
add_page_to_hash_queue		//页放入page cache hashtable

add_page_to_inode_queue		//放入page cache对象address_space的clean_pages队列


全局变量
struct list_head inactive_list;
struct list_head active_list;
	add_page_to_active_list()
	add_page_to_inactive_list()
	del_page_from_active_list()
	del_page_from_inactive_list()

初始化mem_map[]		//paging_init




页目录			//pagetable_init()初始化页表
---------------------------------------
task->mm->pgd

pgd_alloc	pgd_free
pmd_alloc	pmd_free
pte_alloc	pte_free




进程地址空间描述符
-----------------------------------------------
struct mm_struct
{
	struct vm_area_struct * mmap;		/* list of VMAs */
	rb_root_t mm_rb;			//使用红黑树
	struct vm_area_struct * mmap_cache;	/* last find_vma result */
	pgd_t * pgd;				//目录表地址
	atomic_t mm_users;			
	atomic_t mm_count;			
	int map_count;				/* number of VMAs */

	struct list_head mmlist;		/* List of all active mm's.  These are globally strung
						 * together off init_mm.mmlist, and are protected
						 * by mmlist_lock
						 */
}
每个进程有一个内存地址空间的描述符，线程共享一个mm_struct,
新进程从mm_cachep的slab中分配一个描述符


内存区域
----------------------------------------------------------	
struct vm_arae_struct
{
	struct mm_struct * vm_mm;	/* The address space we belong to. */
	unsigned long vm_start;		/* Our start address within vm_mm. */
	unsigned long vm_end;		/* The first byte after our end address within vm_mm. */

	struct vm_area_struct *vm_next;

	pgprot_t vm_page_prot;		/* Access permissions of this VMA. */
	unsigned long vm_flags;		/* Flags, listed below. */

	rb_node_t vm_rb;

	struct vm_area_struct *vm_next_share;
	struct vm_area_struct **vm_pprev_share;
	struct vm_operations_struct * vm_ops;

	struct file * vm_file;		/* File we map to (can be NULL). */
}


