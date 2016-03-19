---
layout:     post
title:      "kenel program"
subtitle:   " \"kernel program\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - linux kernel
---
list.h
LIST_HEAD(name)								//根据name创建链表表头
INIT_LIST_HEAD(struct list_head *list);		//初始化表头节点

list_for_each_entry(pos, head, member)		//

list_add(struct list_head *new, struct list_head *head);
list_add_tail(struct list_head *new, struct list_head *head);
list_del(struct list_head *entry);


IS_ERR
PTR_ERR   //错误号和指针


struct page *alloc_page(gfp_mask)					//分配1个页
struct page *alloc_pages(gfp_mask, int order) 		//分配2order个页	
unsigned long _get_free_page(gfp_mask)				//返回页首的逻辑地址
unsigned long __get_free_pages(gfp_mask, order);	//
unsigned long get_zeroed_page(gfp_mask);			//

free_page(page)
free_pages(unsigned long addr, unsigned int order);
__free_page(page)
__free_pages(struct page *page, unsigned int order);

//alloc mm
void *kmalloc(size_t size, gfp_t flags);			//连续物理地址
void kfree(const void *objp);

void *vmalloc(unsigned long size);					//连续虚拟地址,非连续物理地址
void vfree(const void *addr);


//struct cache in slab
struct kmem_cache *kmem_cache_create (const char *name, size_t size, size_t align,
	unsigned long flags, void (*ctor)(void *));
	
void *kmem_cache_alloc(struct kmem_cache *cachep, gfp_t flags);			//从cache中分配obj
void kmem_cache_free(struct kmem_cache *cachep, void *objp);			//obj 放回cache

void kmem_cache_destroy(struct kmem_cache *cachep);


