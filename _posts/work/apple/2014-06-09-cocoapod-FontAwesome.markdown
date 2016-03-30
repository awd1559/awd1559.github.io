---
layout:     post
title:      "FontAwesome"
subtitle:   " \"FontAwesome\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
[FontAwesome.swift](https://github.com/thii/FontAwesome.swift)

# install

```
use_frameworks!
pod ‘FontAwesome.swift'
```

# usage

```
import FontAwesome_swift//in label
label.font = UIFont.fontAwesomeOfSize(200)
label.text = String.fontAwesomeIconWithName(FontAwesome.Github)

//in label with code
label.font = UIFont.fontAwesomeOfSize(200)
label.text = String.fontAwesomeIconWithCode("fa-github")

//in button
button.titleLabel?.font = UIFont.fontAwesomeOfSize(30)
button.setTitle(String.fontAwesomeIconWithName(.Github), forState: .Normal)

//in navigation bar item
let attributes = [NSFontAttributeName: UIFont.fontAwesomeOfSize(20)] as Dictionary!
leftBarButton.setTitleTextAttributes(attributes, forState: .Normal)
leftBarButton.title = String.fontAwesomeIconWithName(.Github)

//toolbar item
let attributes = [NSFontAttributeName: UIFont.fontAwesomeOfSize(20)] as Dictionary!
toolbarItem.setTitleTextAttributes(attributes, forState: .Normal)
toolbarItem.title = String.fontAwesomeIconWithName(.Github)

//as image
tabBarItem.image = UIImage.fontAwesomeIconWithName(.Github, textColor: UIColor.blackColor(), size: CGSizeMake(30, 30))

//as image with background color
tabBarItem.image = UIImage.fontAwesomeIconWithName(FontAwesome.Github, textColor: UIColor.blueColor(), size: CGSizeMake(4000, 4000), backgroundColor: UIColor.redColor())
```
