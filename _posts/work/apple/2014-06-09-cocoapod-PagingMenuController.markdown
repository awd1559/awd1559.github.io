---
layout:     post
title:      "PagingMenuController"
subtitle:   " \"PagingMenuController\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
>[PagingMenuController](https://github.com/kitasuke/PagingMenuController)
><small>目录:[cocoapod](/2014/06/09/cocoapod-cocoapod)</small>

# install

```
pod 'PagingMenuController'
```

# usage 

- use code 

```
import PagingMenuController

//prepare controllers
let controller1 = First()
let controller2 = Second()
let viewControllers = [controller1, controller2]

//config options
let options = PagingMenuOptions()
options.menuItemMargin = 5
options.menuHeight = 60
options.menuDisplayMode = .SegmentedControl

//
let pagingMenuController = PagingMenuController(viewControllers: viewControllers, options: options)
pagingMenuController.view.frame.origin.y += 64
pagingMenuController.view.frame.size.height -= 64

addChildViewController(pagingMenuController)
view.addSubview(pagingMenuController.view)
pagingMenuController.didMoveToParentViewController(self)
```

- use storyboard

```
let usersViewController = self.storyboard?.instantiateViewControllerWithIdentifier("UsersViewController") as! UsersViewController
let repositoriesViewController = self.storyboard?.instantiateViewControllerWithIdentifier("RepositoriesViewController") as! RepositoriesViewController

let viewControllers = [usersViewController, repositoriesViewController]

let options = PagingMenuOptions()
options.menuHeight = 50
   
let pagingMenuController = self.childViewControllers.first as! PagingMenuController
pagingMenuController.delegate = self
pagingMenuController.setup(viewControllers: viewControllers, options: options)
```

