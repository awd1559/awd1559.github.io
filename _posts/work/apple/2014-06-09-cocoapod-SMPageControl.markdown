---
layout:     post
title:      "SMPageControl"
subtitle:   " \"SMPageControl,几个指示小圆点\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
>[SMPageControl](https://github.com/Spaceman-Labs/SMPageControl)
><small>目录:[cocoapod](/2014/06/09/cocoapod-cocoapod)</small>

```
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
```