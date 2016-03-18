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


