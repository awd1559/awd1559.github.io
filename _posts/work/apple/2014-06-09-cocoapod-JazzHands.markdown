---
layout:     post
title:      "JazzHands"
subtitle:   " \"JazzHands, 启动页滚动介绍页面动画\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
>[JazzHands](https://github.com/IFTTT/JazzHands)
><small>目录:[cocoapod](/2014/06/09/cocoapod-cocoapod)</small>


# install
```
pod "JazzHands"
```

# usage
```
bridege.h
#include "JazzHands/IFTTTJazzHands.h"

import JazzHands

ViewController : IFTTTAnimatedPagingScrollViewController

override func numberOfPages() -> UInt {
  return 4
}

override func viewDidLoad() {
	super.viewDidLoad()
	imageview0 = UIImageView(image: UIImage(named:""))
	contentView.addSubview(imageview0)
	......
	
	keepView(imageview0, onPage:0)	    //show imageview0 on page0
	keepView(imageview1, onPage:1)
	keepView(imageview2, onPages:[2,3])  //show imageview2 on page2 & page3
	keepView(imageview3, onPage:3)
	
	//animations 
	//create animation
	letalphaAnimation = IFTTTAlphaAnimation(view:viewThatYouWantToAnimate)
	//config animation
	alphaAnimation.addKeyframeForTime(30, alpha:1.0)
	alphaAnimation.addKeyframeForTime(60, alpha:0.0)
	//register animator
	self.animator.addAnimation(alphaAnimation)
}
```

|animatioin types                      |property                       |
| ------------------------------------ | ----------------------------- |
|IFTTTAlphaAnimation                   |alpha                          |
|IFTTTRotationAnimation                |a rotation transform in degrees|
|IFTTTBackgroundColorAnimation         |backgroundColor                |
|IFTTTCornerRadiusAnimation            |layer.cornerRadius             |
|IFTTTHideAnimation                    |hidden                         |
|IFTTTScaleAnimation                   |a scaling transform            |
|IFTTTTranslationAnimation             |a translation transform        |
|IFTTTTransform3DAnimation             |layer.transform 3d             |
|IFTTTTextColorAnimation               |textColor                      |
|IFTTTFillColorAnimation               |fillColor                      |
|IFTTTStrokeStartAnimation             |strokeStart of CAShapeLayer    |
|IFTTTStrokeEndAnimation               |strokeEnd of CAShapeLayer      |
|IFTTTPathPositionAnimation            |layer.position                 |
|IFTTTConstraintConstantAnimation      |constraint constant            |
|IFTTTConstraintMultiplierAnimation    |                               |
|IFTTTScrollViewPageConstraintAnimation|                               |
|IFTTTFrameAnimation                   |frame                          |


IFTTTAlphaAnimation
[animation addKeyframeForTime:1.06f alpha:0];
[animation addKeyframeForTime:1.08f alpha:1];
[animation addKeyframeForTime:2.5f alpha:1];
[animation addKeyframeForTime:3.f alpha:0];

IFTTTRotationAnimation
[animation addKeyframeForTime:0 rotation:0];
[animation addKeyframeForTime:1 rotation:100];

IFTTPScaleAnimation
[animation addKeyframeForTime:0 scale:1 withEasingFunction:IFTTTEasingFunctionEaseInQuad];
[animation addKeyframeForTime:1 scale:6];

IFTTTBackgroundColor
[animation addKeyframeForTime:0 color:UIColor.redColor()];
[animation addKeyframeForTime:1 color:UIColor.blueColor()];

IFTTTCornerRadiusAnimation

IFTTTHideAnimation
IFTTTHideAnimation *animation = [IFTTTHideAnimation animationWithView:self.circle hideAt:1.15];

IFTTTTranslationAnimation
animation addKeyframeForTime:0 translation:(CGPoint)


IFTTTTransform3DAnimation

IFTTTTextColorAnimation

IFTTTFillColorAnimation

IFTTTStrokeStartAnimation

IFTTTPathPositionAnimation

IFTTTConstraintConstantAnimation
NSLayoutConstraint *c1
NSLayoutConstraint *c2


IFTTTConstraintMultiplierAnimation

IFTTTScrollViewPageConstraintAnimation

IFTTTFrameAnimation