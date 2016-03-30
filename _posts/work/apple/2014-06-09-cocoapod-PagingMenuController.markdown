---
layout:     post
title:      "PagingMenuController"
subtitle:   " \"PagingMenuController\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
[PagingMenuController](https://github.com/kitasuke/PagingMenuController)

# install
pod 'PagingMenuController'

# usage 

- use code 

```
import PagingMenuController

let controller1 = First()
let controller2 = Second()
let viewControllers = [controller1, controller2]

let options = PagingMenuOptions()
options.menuItemMargin = 5
options.menuHeight = 60
options.menuDisplayMode = .SegmentedControl

let pagingMenuController = PagingMenuController(viewControllers: viewControllers, options: options)
pagingMenuController.view.frame.origin.y += 64
pagingMenuController.view.frame.size.height -= 64
        
addChildViewController(pagingMenuController)
view.addSubview(pagingMenuController.view)
pagingMenuController.didMoveToParentViewController(self)
```

- use storyboard

```
```