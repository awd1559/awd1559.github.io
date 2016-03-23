---
layout:     post
title:      "MJRefresh"
subtitle:   " \"MJRefresh\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
#[MJRefresh](https://github.com/CoderMJLee/MJRefresh)

## install
>pod ‘MJRefresh'


```swift
import MJRefresh

class MyViewController : UITableViewController {

//默认hedaer
var header = MJRefreshNormalHeader(refreshingBlock:{})
```

//带动画图片的header
// 设置回调（一旦进入刷新状态，就调用target的action，也就是调用self的loadNewData方法）
MJRefreshGifHeader *header = [MJRefreshGifHeader headerWithRefreshingTarget:self refreshingAction:@selector(loadNewData)];
// 设置普通状态的动画图片
[header setImages:idleImages forState:MJRefreshStateIdle];
// 设置即将刷新状态的动画图片（一松开就会刷新的状态）
[header setImages:pullingImages forState:MJRefreshStatePulling];
// 设置正在刷新状态的动画图片
[header setImages:refreshingImages forState:MJRefreshStateRefreshing];
// 设置header
self.tableView.mj_header = header;



// 隐藏时间
header.lastUpdatedTimeLabel.hidden = YES;

// 隐藏状态
header.stateLabel.hidden = YES;
// 设置文字
[header setTitle:@"Pull down to refresh" forState:MJRefreshStateIdle];
[header setTitle:@"Release to refresh" forState:MJRefreshStatePulling];
[header setTitle:@"Loading ..." forState:MJRefreshStateRefreshing];

// 设置字体
header.stateLabel.font = [UIFont systemFontOfSize:15];
header.lastUpdatedTimeLabel.font = [UIFont systemFontOfSize:14];

// 设置颜色
header.stateLabel.textColor = [UIColor redColor];
header.lastUpdatedTimeLabel.textColor = [UIColor blueColor];









}