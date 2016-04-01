---
layout:     post
title:      "Autolayout"
subtitle:   " \"Autolayout\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - iOS
---

# views

```
let headerView = UIView()
let avatar = UIImageView()
let nameLabel = UILabel()
headerView.addSubview(avatar)
headerView.addSubview(nameLabel)

let views = ["avatar":avatar, "nameLabel":nameLabel]
```

# VisualFormat

```
// avatar.height = 60
headerView.addConstraints(NSLayoutConstraint.constraintsWithVisualFormat(
    "V:[avatar(60)]-10-[nameLabel]-15-|",
    options:.AlignAllCenterX,
    metrics:nil,
    views:views))
```

## matrics

```
//1/4 width － 15
let metrics = ["x": UIScreen.mainScreen().bounds.size.width / 4 - 15]
//到left,1/4 width - 15, avatar.width = 60
headerView.addConstraints(NSLayoutConstraint.constraintsWithVisualFormat(
    "|-x-[avatar(60)]",
    options:[],
    metrics:metrics,
    views:views))
```

# item

```
//logo.centerx = view.centerx * 1 + 0
self.view.addConstraint(NSLayoutConstraint(item:logo,      
    attribute:NSLayoutAttribute.CenterX,
    relatedBy:NSLayoutRelation.Equal,
    toItem:self.view,
    attribute:NSLayoutAttribute.CenterX,
    multiplier:1.0,
    constant:0))
```
