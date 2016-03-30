---
layout:     post
title:      "RDVTabBarController"
subtitle:   " \"RDVTabBarController\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
RDVTabBarController
https://github.com/robbdimitrov/RDVTabBarController

install
pod 'RDVTabBarController'


//使用
TabBar
UIViewController* first = [[FirstViewController alloc]init];
UIViewController* second = [[SecondViewController alloc]init];
UIViewController* third = [[ThirdViewController alloc]init];

#import "RDVTabBarController.h"
RDVTabBarController* tab = [[RDVTabBarController alloc]init];
[tab setViewControllers:@[first, second, third]];




//swift
bridge.h
#import “RDVTabBarController/RDVTabBarController.h"
#import “RDVTabBarController/RDVTabBarItem.h"

import RDVTabBarController
let first = FirstViewController()
let second = SecondViewController()
let tab = RDVTabBarController()
tab.viewControllers = [first, second]

//自定义
let tabImages = ["first", "second"]
for (idx, item) in tab.tabBar.items.enumerate() {
	let realItem = item as! RDVTabBarItem
	let image = UIImage(named: tabImages[idx])
	realItem.setFinishedSelectedImage(image, withFinishedUnselectedImage: image)
}

self.window.rootViewController = tab




//自定义
#import "RDVTabBarItem.h"
RDVTabBar* bar = [tab tabBar];
for (RDVTabBarItem *item in [bar items])
	item.titlePositionAdjustment = UIOffsetMake(-10, 5);
	[item setTitle:@""];
	[item setBadgeValue:@"1"];
	[item setBackgroundSelectedImage:backgroundImage withUnselectedImage:backgroundImage];
	[item setFinishedSelectedImage:selectedImage withFinishedUnselectedImage:unselectedImage];
