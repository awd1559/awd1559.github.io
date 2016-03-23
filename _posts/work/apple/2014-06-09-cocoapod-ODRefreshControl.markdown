---
layout:     post
title:      "ODRefreshControl"
subtitle:   " \"ODRefreshControl\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
ODRefreshControl
https://github.com/Sephiroth87/ODRefreshControl
下拉刷新
#import "ODRefreshControl.h"
ODRefreshControl *refreshControl = [[ODRefreshControl alloc] initInScrollView:self.scrollView];
//回调：
[refreshControl addTarget:self action:@selector(dropViewDidBeginRefreshing:) forControlEvents:UIControlEventValueChanged];
//下拉
[refreshControl beginRefreshing];
//下拉结束
[refreshControl endRefreshing];

SVPullToRefresh
https://github.com/samvermette/SVPullToRefresh
pod 'SVPullToRefresh'
