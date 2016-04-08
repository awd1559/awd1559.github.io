---
layout:     post
title:      "pop"
subtitle:   " \"pop\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
>[pop](https://github.com/facebook/pop)
><small>目录:[cocoapod](/2014/06/09/cocoapod-cocoapod)</small>

# install
```
pod 'pop'
```


PopBasicAnimation
PopSpringAnimation
PopDecayAnimation
PopCustomAnimation

```
let animation = POPBasicAnimation(propertyNamed: kPOPViewAlpha)
animation.fromValue = 0
animation.toValue = 1
animation.duration = 2
view.pop_addAnimation(animation, forKey: "fade")

let spring = POPSpringAnimation(propertyNamed: kPOPLayerOpacity)
spring.toValue = 0
spring.beginTime = CACurrentMediaTime() + 2
spring.springBounciness = 10.0  //[0-20] 弹力
spring.springSpeed = 10.0       //[0-20] 速度
spring.dynamicsTension = 0      //拉力
spring.dynamicsFriction = 0     //摩擦
spring.dynamicsMass     = 0     //质量
sender.layer.pop_addAnimation(spring, forKey: "fade")

let decay = POPDecayAnimation(propertyNamed: kPOPLayerOpacity)
decay.velocity = 600
decay.beginTime = CACurrentMediaTime() + 4
decay.deceleration = 0.998  //衰减系数
decay.layer.pop_addAnimation(decay, forKey: "fade")
```


```
/**
 Common CALayer property names.
 */
public let kPOPLayerBackgroundColor: String
public let kPOPLayerBounds: String
public let kPOPLayerCornerRadius: String
public let kPOPLayerBorderWidth: String
public let kPOPLayerBorderColor: String
public let kPOPLayerOpacity: String
public let kPOPLayerPosition: String
public let kPOPLayerPositionX: String
public let kPOPLayerPositionY: String
public let kPOPLayerRotation: String
public let kPOPLayerRotationX: String
public let kPOPLayerRotationY: String
public let kPOPLayerScaleX: String
public let kPOPLayerScaleXY: String
public let kPOPLayerScaleY: String
public let kPOPLayerSize: String
public let kPOPLayerSubscaleXY: String
public let kPOPLayerSubtranslationX: String
public let kPOPLayerSubtranslationXY: String
public let kPOPLayerSubtranslationY: String
public let kPOPLayerSubtranslationZ: String
public let kPOPLayerTranslationX: String
public let kPOPLayerTranslationXY: String
public let kPOPLayerTranslationY: String
public let kPOPLayerTranslationZ: String
public let kPOPLayerZPosition: String
public let kPOPLayerShadowColor: String
public let kPOPLayerShadowOffset: String
public let kPOPLayerShadowOpacity: String
public let kPOPLayerShadowRadius: String

/**
 Common CAShapeLayer property names.
 */
public let kPOPShapeLayerStrokeStart: String
public let kPOPShapeLayerStrokeEnd: String
public let kPOPShapeLayerStrokeColor: String
public let kPOPShapeLayerFillColor: String
public let kPOPShapeLayerLineWidth: String
public let kPOPShapeLayerLineDashPhase: String

/**
 Common NSLayoutConstraint property names.
 */
public let kPOPLayoutConstraintConstant: String

/**
 Common UIView property names.
 */
public let kPOPViewAlpha: String
public let kPOPViewBackgroundColor: String
public let kPOPViewBounds: String
public let kPOPViewCenter: String
public let kPOPViewFrame: String
public let kPOPViewScaleX: String
public let kPOPViewScaleXY: String
public let kPOPViewScaleY: String
public let kPOPViewSize: String
public let kPOPViewTintColor: String

/**
 Common UIScrollView property names.
 */
public let kPOPScrollViewContentOffset: String
public let kPOPScrollViewContentSize: String
public let kPOPScrollViewZoomScale: String
public let kPOPScrollViewContentInset: String
public let kPOPScrollViewScrollIndicatorInsets: String

/**
 Common UITableView property names.
 */
public let kPOPTableViewContentOffset: String
public let kPOPTableViewContentSize: String

/**
 Common UICollectionView property names.
 */
public let kPOPCollectionViewContentOffset: String
public let kPOPCollectionViewContentSize: String

/**
 Common UINavigationBar property names.
 */
public let kPOPNavigationBarBarTintColor: String

/**
 Common UIToolbar property names.
 */
public let kPOPToolbarBarTintColor: String

/**
 Common UITabBar property names.
 */
public let kPOPTabBarBarTintColor: String

/**
 Common UILabel property names.
 */
public let kPOPLabelTextColor: String

```
