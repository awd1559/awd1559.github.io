---
layout:     post
title:      "FXBlurView"
subtitle:   " \"cocopods, FXBlurView, 使得背景模糊\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
>[FXBlurView](https://github.com/nicklockwood/FXBlurView)
><small>目录:[cocoapod](/2014/06/09/cocoapod-cocoapod)</small>


# install

```
pod 'FXBlurView', '~> 1.6.4'

//only have two files: FXBlurView.h, FXBlurView.m
```

# usage

```
import FXBlurView

let frostedView = FXBlurView()
frostedView.underlyingView = UIImageView(image:UIImage(named:""))
frostedView.dynamic = false
frostedView.tintColor = UIColor.blackColor()
frostedView.frame = CGRect(x:0.0, y:view.frame.height/2, width:view.frame.width, height:view.frame.height/2)
view.addSubview(frostedView) 

//add some view to show
let someview = UIView()
someview.frame = frostedView.frame
view.addSubview(someview)
```
