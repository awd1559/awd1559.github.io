---
layout:     post
title:      "pop"
subtitle:   " \"pop\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
https://github.com/facebook/pop

BasicAnimation
SpringAnimation
DecayAnimation
CustomAnimation

pod “pop”
#import “POP.h”

POPCustomAnimation
POPPropertyAnimation
	POPDecayAnimation
	POPSpringAnimation
	POPBasicAnimation

//fade 
POPBasicAnimation *anim = [POPBasicAnimation animationWithPropertyNamed:kPOPViewAlpha];
anim.fromValue = @(0.0);
anim.toValue = @(1.0);
aim.duration = 2.0f;
[view pop_addAnimation:anim forKey:@“fade”];


//xy scale
POPSpringAnimation *anim = [POPSpringAnimation animationWithPropertyNamed:kPOPLayerScaleXY];
anim.toValue = [NSValue valueWithCGPoint:CGPointMake(arc4random()%2+1, arc4random()%2+1)];
//spring animation 必须添加类似如下参数
//反弹
anim.springBounciness = 4.0;
//速度
anim.springSpeed = 12.0;
//拉力
anim.dynamicsTension = 
//摩擦力
anim.dynamicsFriction = 
//质量
anime.dynamicsMass

anim.completionBlock = ^(POPAnimation *anim, BOOL finished) {if (finished) {NSLog(@"Animation finished!”);}};
//BasicAnimation也可以作用于layer
[self.lbl.layer pop_addAnimation:anim forKey:@“size"];

//move to
POPSpringAnimation *anim = [POPSpringAnimation animationWithPropertyNamed:kPOPLayerBounds];
anim.toValue = [NSValue valueWithCGRect:CGRectMake(0, 0, 400, 400)];
anim.springBounciness = 4.0;
anim.springSpeed = 12.0;
[layer pop_addAnimation:anim forKey:@“size"];






//衰减，从x坐标的25开始按照100/s的速度做减速运动
POPDecayAnimation *anim = [POPDecayAnimation animationWithPropertyNamed:kPOPLayerPositionX];
anim.velocity = @(100.0);
anim.fromValue = @(25.0);
[layer pop_addAnimation:anim forKey:@“slide"];


