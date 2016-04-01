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

```
view.translatesAutoresizingMaskIntoConstraints = false
```

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

Visual Format Language
```
H:[button]-[textField]		标准间距
H:[button]—8-[textField]	水平间距8
H:[button(>=50)]		button.width >=50
H:|-50-[box]-50-|		距左边50，右边50；
V:[topField]-10-[buttonField]	垂直间距10

[maroonView][oceanView]		Flush Views
[button(100@20)]		Priority
[button1(==button2)]		Equal Widths
[flexButton(>=70, <=100)]
```
