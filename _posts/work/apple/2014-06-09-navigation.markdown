---
layout:     post
title:      "navigation"
subtitle:   " \"navigation\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - iOS
---
UINavigationBar
	UINavigationItem
		UIBarButtonItem


UINavigationController
UINavigationBar
UINavigationItem


//切换到子viewcontroller中
//TODO:默认动画为Push，如何自定义动画
[self.navigationController pushViewController:detailViewController animated:YES];

//动画弹出viewController
viewController.modalTransitionStyle = UIModalTransitionStyleCrossDissolve;
[self.navigationController presentViewController:detail animated:YES completion:NULL];设置navigation button
UINavigationController *nav = [[UINavigationController alloc] initWithRootViewController:myviewcontroller];

nav.modalTransitionStyle = UIModalTransitionStyleFlipHorizontal;
[self presentViewController:nav animated:YES completion:nil];

myviewcontroller : UIViewController
UIButton *button = [[UIButton alloc] init];
[button setTitle:@""];

[button setTitleColor:[] forState:UIControlStateNormal];
[button setTitleColor:[] forState:UIControlStateDisabled];

button.titleLabel setFont:[UIFont systemFontOfSize:17]
[button sizeToFit];

[button addTarget:self action:@selector(back) forControlEvents:UIControlEventTouchUpInside];

self.navigationItem.leftBarButtonItem = [[UIBarButtonItem alloc] initWithCustomView:button];

-(void)back
    [self.dismissViewControllerAnimated:YES completion:nil];
