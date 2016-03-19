---
layout:     post
title:      "filesystem"
subtitle:   " \"filesystem\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - linux kernel
---
全局super_blocks列表	(fs/supper.c)	所有supper_block通过s_list连接起来管理

supper_block
{
	... ...
	struct list_head	s_list;
	kdev_t			s_dev;
	
	struct file_system_type	*s_type;
	struct super_operations	*s_op;
	struct dquot_operations	*dq_op;
	
	struct dentry		*s_root;
	struct list_head	s_dirty;			//inodes list
	struct list_head	s_locked_inodes;	
	struct list_head	s_files;			//

	struct block_device	*s_bdev;
	
	union {
		.. ..
		struct ext2_sb_info	ext2_sb;
		struct ext3_sb_info	ext3_sb;
		.. ..
	}u;
	... ...
}