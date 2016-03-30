---
layout:     post
title:      "PopMenu"
subtitle:   " \"PopMenu\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
PopMenu
https://github.com/xhzengAIB/PopMenu

pod 'PopMenu'
NSArray *items = @[
	[MenuItem itemWithTitle:@"项目" iconName:@"pop_Project" index:0],
        [MenuItem itemWithTitle:@"任务" iconName:@"pop_Task" index:1],
        [MenuItem itemWithTitle:@"冒泡" iconName:@"pop_Tweet" index:2],
        [MenuItem itemWithTitle:@"添加好友" iconName:@"pop_User" index:3],
        [MenuItem itemWithTitle:@"私信" iconName:@"pop_Message" index:4],
        [MenuItem itemWithTitle:@"两步验证" iconName:@"pop_2FA" index:5],
];
PopMenu *popMenu = [[PopMenu alloc] initWithFrame:self.view.bounds items:items];
popMenu.menuAnimationType = kPopMenuAnimationTypeNetEase; // kPopMenuAnimationTypeSina
popMenu.perRowItemCount = 3; // or 2
[popMenu showMenuAtView:self.view];

popMenu.didSelectedItemCompletion = ^(MenuItem *selectedItem) {
	switch(selectedItem.index)
}
