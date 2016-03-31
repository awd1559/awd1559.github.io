---
layout:     post
title:      "FXBlurView"
subtitle:   " \"FXBlurView, 背景模糊\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
[FXBlurView](https://github.com/nicklockwood/FXBlurView)

# not tested 

# install

```
pod 'FXBlurView', '~> 1.6.4'
```

# usage

```
import FXBlurView
let frostedView = FXBlurView()
frostedView.underlyingView = self.backgroundImageView!
frostedView.dynamic = false
frostedView.tintColor = UIColor.blackColor()
frostedView.frame = self.view.frame
self.view.addSubview(frostedView) 
```
