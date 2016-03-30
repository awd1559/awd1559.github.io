---
layout:     post
title:      "SMPageControl"
subtitle:   " \"SMPageControl\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
SMPageControl
几个指示小圆点
https://github.com/Spaceman-Labs/SMPageControl

@property (strong, nonatomic) SMPageControl *pageControl;

self.pageControl = ({
        SMPageControl *pageControl = [[SMPageControl alloc] init];
        pageControl.numberOfPages = self.numberOfPages;
        pageControl.userInteractionEnabled = NO;
        pageControl.pageIndicatorImage = pageIndicatorImage;
        pageControl.currentPageIndicatorImage = currentPageIndicatorImage;
        [pageControl sizeToFit];
        pageControl.currentPage = 0;
        pageControl;
});
[self.view addSubview:self.pageControl];
