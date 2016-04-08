---
layout:     post
title:      "DrawerController"
subtitle:   " \"DrawerController\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---

>[DrawerController](https://github.com/sascha/DrawerController)
><small>目录:[cocoapod](/2014/06/09/cocoapod-cocoapod)</small>

# install 

```
platform :ios, '8.0'
use_frameworks!

pod 'DrawerController', '~> 1.0'
```

# usage 

```
import DrawerController

//setup left and content controller
let centerNav = UINavigationController(rootViewController: HomeViewController())
let leftViewController = LeftViewController()
let rightViewController = RightViewController()

let drawerController = DrawerController(
  centerViewController: centerNav, 
  leftDrawerViewController: leftViewController,
  rightDrawerViewController: rightViewController)

drawerController.maximumLeftDrawerWidth=230
drawerController.maximumRightDrawerWidth=110
drawerController.openDrawerGestureModeMask=OpenDrawerGestureMode.PanningCenterView
drawerController.closeDrawerGestureModeMask=CloseDrawerGestureMode.All


self.window?.rootViewController = drawerController
```

in ViewController

```
//setup content controller navigation item
func setupNavigationItem(){
  let leftButton = NotificationMenuButton()
  leftButton.frame = CGRectMake(0, 0, 40, 40)
  self.navigationItem.leftBarButtonItem = UIBarButtonItem(customView: leftButton)
  leftButton.addTarget(self, action: Selector("leftClick"), forControlEvents: .TouchUpInside)
      
  let rightButton = UIButton(frame: CGRect(x:0, y:0, width:40, height:40))
  rightButton.contentMode = .Center
  rightButton.imageEdgeInsets = UIEdgeInsetsMake(0, 0, 0, -15)
  rightButton.setImage(UIImage.imageUsedTemplateMode("ic_more_horiz_36pt")!.imageWithRenderingMode(.AlwaysTemplate), forState: .Normal)
  self.navigationItem.rightBarButtonItem = UIBarButtonItem(customView: rightButton)
  rightButton.addTarget(self, action: Selector("rightClick"), forControlEvents: .TouchUpInside)
}
```

Selector

```
//get drawerController instance
func leftClick(){
	self.evo_drawerController?.toggleLeftDrawerSideAnimated(true, completion: nil)
}
func rightClick(){
	self.evo_drawerController?.toggleRightDrawerSideAnimated(true, completion: nil)
}

//get center view controller
self.evo_drawerController?.centerViewController
```

