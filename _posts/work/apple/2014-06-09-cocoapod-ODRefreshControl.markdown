---
layout:     post
title:      "ODRefreshControl"
subtitle:   " \"ODRefreshControl,下拉刷新\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
>[ODRefreshControl](https://github.com/Sephiroth87/ODRefreshControl)
><small>目录:[cocoapod](/2014/06/09/cocoapod-cocoapod)</small>


```
#import "ODRefreshControl.h"

ODRefreshControl *refreshControl = [[ODRefreshControl alloc] initInScrollView:self.scrollView];

[refreshControl addTarget:self action:@selector(dropViewDidBeginRefreshing:) forControlEvents:UIControlEventValueChanged];

[refreshControl beginRefreshing];
[refreshControl endRefreshing];
```
