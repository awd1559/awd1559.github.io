---
layout:     post
title:      "PagingMenuController"
subtitle:   " \"PagingMenuController\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
>[PageMenu](https://github.com/HighBay/PageMenu)
><small>目录:[cocoapod](/2014/06/09/cocoapod-cocoapod)</small>

# install

```
pod 'PageMenu'
```

# usage

```
import PageMenu
var pageMenu : CAPSPageMenu?
var controllers : [UIViewController] = []
let c1 = FirstViewController()
c1.title = ""
let c2 = SecondViewcontroller()
c2.title = ""
controllers.append(c1)
controllers.append(c2)

var parameters: [CAPSPageMenuOption] = [
    .MenuItemSeparatorWidth(4.3), 
    .UseMenuLikeSegmentedControl(true), 
    .MenuItemSeparatorPercentageHeight(0.1)
]

pageMenu = CAPSPageMenu(viewControllers: controllers, frame: CGRectMake(0.0, 0.0, self.view.frame.width, self.view.frame.height), pageMenuOptions: parameters)

self.view.addSubview(pageMenu!.view)
```

