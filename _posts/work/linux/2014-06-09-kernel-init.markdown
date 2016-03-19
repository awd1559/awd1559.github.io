---
layout:     post
title:      "kernel init"
subtitle:   " \"kernel init\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - linux kernel
---
start_kernel
	->setup_arch
		->setup_memory_region		//读e820图
		->setup_memory			//
			->find_max_pfn		//找到max_pfn
			->find_max_low_pfn	//找到max_low_pfn
			->init_bootmem(max_low_pfn, min_low_pfn)	
							//初始化引导内存管理器的位图数据
				->init_bootmem_core(contig_page_data, )
					-pgdat_list = contig_page_data;
					-memset(bdata->node_bootmem_map, 0xff, mapsize);
			->reserve_bootmem		//保留一些必要的引导内存
				->reserve_bootmem_core	

		->paging_init
			->pagetable_init		//初始化页表
			->load_cr3(swapper_pg_dir); 	//加载页表地址到cr3
			->__flush_tlb_all		//刷新tlb
			->kmap_init			
			->zone_sizes_init		
				->free_area_init(long zone_size[3])	//初始化伙伴算法列表
					->build_zonelists		//从哪个zone开始分配
									//以上内存只能从引导内存分配器中分配
									//alloc_bootmem_*->__alloc_bootmem
		->register_memory
			->request_resource		//初始化多个*_resource列表




