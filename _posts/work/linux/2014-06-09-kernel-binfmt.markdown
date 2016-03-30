---
layout:     post
title:      "binfmt"
subtitle:   " \"bin format\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - linux kernel
---
static struct linux_binfmt *formats;	//全局(exec.c)
... ...
static struct linux_binfmt aout_format;	//(fs/binfmt_aout.c)
static struct linux_binfmt elf_format;	//(fs.binfmt_elf.c)
... ...
//通过register_binfmt()连接到formats;
