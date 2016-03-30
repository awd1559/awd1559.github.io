---
layout:     post
title:      "resources"
subtitle:   " \"resources\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - iOS
---
[NSBundle mainBundle]pathForResource:@"my.plist" ofType:nil];
my.plist应该是在group中，而不是reference的，reference的资源编译时不会放到pkg文件中


//读取文件
NSBundle *bundle = [NSBundle mainBundle];
	NSString *plistPath = [bundle pathForResource:@"team"
                                           ofType:@"plist"];
//获取属性列表文件中的全部数据
self.listTeams = [[NSArray alloc] initWithContentsOfFile:plistPath];    


preview中有:
3.5英寸
4英寸
4.7英寸
5.5英寸
iPad 1/3
iPad 1/2
iPad 2/3
iPad


