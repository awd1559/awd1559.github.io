---
layout:     post
title:      "Animo"
subtitle:   " \"animo,Animation\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
>[Animo](https://github.com/eure/Animo)
><small>目录:[cocoapod](/2014/06/09/cocoapod-cocoapod)</small>

# install
```
pod 'Animo'
```

# usage

Animo turns this:
```
let positionAnimation = CABasicAnimation(keyPath: "position")
positionAnimation.fromValue = NSValue(CGPoint: fromPoint)
positionAnimation.toValue = NSValue(CGPoint: toPoint)

let colorAnimation = CABasicAnimation(keyPath: "backgroundColor")
colorAnimation.fromValue = fromColor.CGColor
colorAnimation.toValue = toColor.CGColor

let animationGroup = CAAnimationGroup()
animationGroup.animations = [positionAnimation, colorAnimation]
animationGroup.fillMode = kCAFillModeForwards
animationGroup.removedOnCompletion = false
animationGroup.timingFunction = CAMediaTimingFunction(name: kCAMediaTimingFunctionEaseInEaseOut)

someView.layer.addAnimation(animationGroup, forKey: "animationGroup")
```

to this:
```
someView.layer.runAnimation(
    Animo.group(
        Animo.move(from: fromPoint, to: toPoint, duration: 1),
        Animo.keyPath("backgroundColor", from: fromColor, to: toColor, duration: 1),
        timingMode: .EaseInOut,
        options: Options(fillMode: .Forwards)
    )
)
```


api
```
group(...)
sequence(...)
autoreverse(...)
wait(...)
replay(...) and replayForever(...)

Animo.move()
Animo.translate
Animo.scale
Animo.fade
Animo.keyPath()
```
