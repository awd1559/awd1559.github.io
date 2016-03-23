---
layout:     post
title:      "RKSwipeBetweenViewController"
subtitle:   " \"RKSwipeBetweenViewController\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
RKSwipeBetweenViewControllers
https://github.com/cwRichardKim/RKSwipeBetweenViewControllers

//install
pod 'RKSwipeBetweenViewControllers'


UIPageViewController *pageController = [[UIPageViewController alloc] initWithTransitionStyle:UIPageViewControllerTransitionStyleScroll   navigationOrientation:UIPageViewControllerNavigationOrientationHorizontal options:nil];
    
RKSwipeBetweenViewControllers *nav = [[RKSwipeBetweenViewControllers alloc]initWithRootViewController:pageController];

[nav.viewControllerArray addObjectsFromArray:@[ first, second, third]];
nav.buttonText = @[@"冒泡广场", @"朋友圈", @“热门冒泡"];


//swift
bridge.h
#import <RKSwipeBetweenViewControllers/RKSwipeBetweenViewControllers.h>

import RKSwipeBetweenViewControllers

let second = SecondViewController()
let third = ThirdViewController()
let four = FourViewController()

let pagerController = UIPageViewController(transitionStyle: .Scroll, navigationOrientation: .Horizontal, options: nil)
let nav = RKSwipeBetweenViewControllers(rootViewController: pagerController)
nav.viewControllerArray.addObjectsFromArray([second, third, four])
nav.buttonText = ["冒泡广场", "朋友圈", “热门冒泡"]




/自定义