---
layout:     post
title:      "JazzHands"
subtitle:   " \"JazzHands\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
启动页滚动介绍页面动画
https://github.com/IFTTT/JazzHands

//install
pod "JazzHands"

#import <IFTTTJazzHands.h>

ViewController : IFTTTAnimatedPagingScrollViewController

- (NSUInteger)numberOfPages
{
    return 4;
}

-(void)viewDidLoad {
	[super viewDidLoad]
	[self configViews]
	[self configAnimations]
}
-(void)configViews {
	self.imageview0 = [[UIImageView alloc]initWithImage:[UIImage imageNamed:@"intro_icon_0.png"]];
	[self.contentView addSubview:self.imageview0];
	.............
}
-(void)configAnimations {
	[self keepView:self.imageview0 onPage:0];
	[self keepView:self.imageview1 onPage:1];
	[self keepView:self.imageview2 onPage:2];
	[self keepView:self.imageview3 onPage:3];

	//animations 
	//create animation
	IFTTTAlphaAnimation *alphaAnimation = [IFTTTAlphaAnimation animationWithView: viewThatYouWantToAnimate];
	//config animation
	[alphaAnimation addKeyframeForTime:30 alpha:1.f];
	[alphaAnimation addKeyframeForTime:60 alpha:0.f];
	//register animator
	[self.animator addAnimation: alphaAnimation];
}

其中animation有很多变化
//imageview0 y 对齐到一个高度
[self.imageview0 mas_makeConstraints:^(MASConstraintMaker *make) {
        make.centerY.mas_equalTo(-kScreen_Height/6);
}];
//tipview.top = imageview.bottom +  45
[self.tipview0 mas_makeConstraints:^(MASConstraintMaker *make) {
        make.top.equalTo(self.imageview0.mas_bottom).offset(kScaleFrom_iPhone5_Desgin(45));
}];
//imageview0 在第0页和第1页显示
[self keepView:self.imageview0 onPages:@[@(0), @(1)]];

//为各个view设置animation
IFTTT*Animation *animation = [IFTTT*Animation animationWithView:view];
[animation addKeyframe           ]
[self.animator addAnimation:animation];

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
[animation addKeyframeForTime:0 color:[UIColor colorWithRed:0.4f green:0.4f blue:0.4f alpha:1.f]];
[animation addKeyframeForTime:1 color:[UIColor colorWithRed:0.14f green:0.8f blue:1.f alpha:1.f]];

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