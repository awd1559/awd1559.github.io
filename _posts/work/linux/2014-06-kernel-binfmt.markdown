---
layout:     post
title:      "shell"
subtitle:   " \"shell脚本\""
date:       2015-01-29 12:00:00
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
