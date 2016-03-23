---
layout: post
title: MJRefresh
subtitle: " \"MJRefresh\""
date: {}
author: awd
"header-img": "img/post-bg-2015.jpg"
tags: 
  - cocoapod
published: true
---

#[MJRefresh](https://github.com/CoderMJLee/MJRefresh)

## install
```swift
pod	'MJRefresh'
```

## get start
```swift
import MJRefresh
```
## api
###### MJRefreshsComponent.h
```swift
	//进入刷新状态
 	beginRefreshing()
 	//结束刷新
 	endRefreshing()
 	//是否在刷新
 	isRefreshing() -> Bool
```
###### MJRefreshHeader.h
```swift
	//创建header
	headerWithRefreshingBlock(MJRefreshComponentRefreshingBlock) -> MJRefreshHeader
	headerWithRefreshingTarget(target, refreshingAction action:SEL) -> MJRefreshHeader
	lastUpdatedTimeKey:String
	lastUpdatedTime:NSDate
```
###### MJRefreshFooter.h
```swift
	footerWithRefreshingBlock(MJRefreshComponentRefreshingBlock)
	footerWithRefreshingTarget(target, refreshingAction:SEL)
	endRefreshingWithNoMoreDate()
	resetNoMoreData()	
```
###### MJRefreshAutoFooter.h


## examples
###### 下拉刷新
- default
```swift
self.tableView.header = MJRefreshNormalHeader.headerWithRefreshingBlock{
	//进入刷新状态后会自动调用这个block
}
self.tableView.header = MJRefreshNormalHeader.headerWithRefreshingTarget(self, refreshingAction:Selector("loadNewData"))
self.tableView.header.beginRefreshing()
```

- animation
```objc
//设置回调（一旦进入刷新状态，就调用target的action，也就是调用self的loadNewData方法）
MJRefreshGifHeader *header = [MJRefreshGifHeader headerWithRefreshingTarget:self refreshingAction:@selector(loadNewData)];
//设置普通状态的动画图片
[header setImages:idleImages forState:MJRefreshStateIdle];
//设置即将刷新状态的动画图片（一松开就会刷新的状态）
[header setImages:pullingImages forState:MJRefreshStatePulling];
// 设置正在刷新状态的动画图片
[header setImages:refreshingImages forState:MJRefreshStateRefreshing];
// 设置header
self.tableView.mj_header = header;
```

- hide time label
```swift
header.lastUpdatedTimeLabel.hidden = true
```

- hide status and time
```swift
// 隐藏时间
header.lastUpdatedTimeLabel.hidden = true
// 隐藏状态
header.stateLabel.hidden = true
```

- custome text
```swift
// 设置文字
header.setTitle("Pull down to refresh", forState:MJRefreshStateIdle)
header.setTitle("Release to refresh", forState:MJRefreshStatePulling)
header.setTitle("Loading ...", forState:MJRefreshStateRefreshing)

// 设置字体
header.stateLabel.font = UIFont.systemFontOfSize(15)
header.lastUpdatedTimeLabel.font = UIFont.systemFontOfSize(14)

// 设置颜色
header.stateLabel.textColor = UIColor.redColor()
header.lastUpdatedTimeLabel.textColor = UIColor.blueColor()
```
- custome view 
```objc
self.tableView.mj_header = [MJDIYHeader headerWithRefreshingTarget:self refreshingAction:@selector(loadNewData)];
// 具体实现参考MJDIYHeader.h和MJDIYHeader.m
```


###### 上拉刷新
- default
```objc
self.tableView.mj_footer = [MJRefreshAutoNormalFooter footerWithRefreshingBlock:^{
   // 进入刷新状态后会自动调用这个block
}];
或
// 设置回调（一旦进入刷新状态，就调用target的action，也就是调用self的loadMoreData方法）
self.tableView.mj_footer = [MJRefreshAutoNormalFooter footerWithRefreshingTarget:self refreshingAction:@selector(loadMoreData)];
```

- animation
```objc
// 设置回调（一旦进入刷新状态，就调用target的action，也就是调用self的loadMoreData方法）
MJRefreshAutoGifFooter *footer = [MJRefreshAutoGifFooter footerWithRefreshingTarget:self refreshingAction:@selector(loadMoreData)];

// 设置刷新图片
[footer setImages:refreshingImages forState:MJRefreshStateRefreshing];

// 设置尾部
self.tableView.mj_footer = footer;
```

- hide refresh text
```swift
// 隐藏刷新状态的文字
footer.refreshingTitleHidden = true
// 如果没有上面的方法，就用footer.stateLabel.hidden = true
```
- load complete
```objc
// 变为没有更多数据的状态
[footer endRefreshingWithNoMoreData];
```
- custome text
```objc
// 设置文字
[footer setTitle:@"Click or drag up to refresh" forState:MJRefreshStateIdle];
[footer setTitle:@"Loading more ..." forState:MJRefreshStateRefreshing];
[footer setTitle:@"No more data" forState:MJRefreshStateNoMoreData];

// 设置字体
footer.stateLabel.font = [UIFont systemFontOfSize:17];

// 设置颜色
footer.stateLabel.textColor = [UIColor blueColor];
```
- hide after load
```objc
// 隐藏当前的上拉刷新控件
self.tableView.mj_footer.hidden = YES;
```
- bounce 01
```objc
self.tableView.mj_footer = [MJRefreshBackNormalFooter footerWithRefreshingTarget:self refreshingAction:@selector(loadMoreData)];
```
- bounce 02
```objc
MJRefreshBackGifFooter *footer = [MJRefreshBackGifFooter footerWithRefreshingTarget:self refreshingAction:@selector(loadMoreData)];

// 设置普通状态的动画图片
[footer setImages:idleImages forState:MJRefreshStateIdle];
// 设置即将刷新状态的动画图片（一松开就会刷新的状态）
[footer setImages:pullingImages forState:MJRefreshStatePulling];
// 设置正在刷新状态的动画图片
[footer setImages:refreshingImages forState:MJRefreshStateRefreshing];

// 设置尾部
self.tableView.mj_footer = footer;
```
- custome view 1
```objc
self.tableView.mj_footer = [MJDIYAutoFooter footerWithRefreshingTarget:self refreshingAction:@selector(loadMoreData)];
// 具体实现参考MJDIYAutoFooter.h和MJDIYAutoFooter.m
```
- custome view 2
```objc
self.tableView.mj_footer = [MJDIYBackFooter footerWithRefreshingTarget:self refreshingAction:@selector(loadMoreData)];
// 具体实现参考MJDIYBackFooter.h和MJDIYBackFooter.m
```

```objc
class MyViewController : UITableViewController {

//默认hedaer
var header = MJRefreshNormalHeader(refreshingBlock:{})

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
```
