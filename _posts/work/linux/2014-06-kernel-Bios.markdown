---
layout:     post
title:      "bios"
subtitle:   " \"bios\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - linux kernel
---
i386加电时，cs = 0xffff， ip=0，这个地址就是Bios所在的地址
Bios读取磁盘的第一个扇区(MBR),到0x7c00处，并执行

BIOS内存分布
==================================================
oxA0000即640KB以上都用于图形接口卡和BIOS本身
oxA0000即640KB一下为系统的基本内存
从0x100000即1MB开始为“高内存”





