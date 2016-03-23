---
layout:     post
title:      "iCarousel"
subtitle:   " \"iCarousel\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
iCarousel
view旋转木马效果	
https://github.com/nicklockwood/iCarousel

添加QuartzCore,默认为不需要添加也可以成功
select project -> target -> build phases -> Link binary with Libraries

只需要iCarousel.h、iCarousel.m两个文件
#import "iCarousel.h"
@interface : UIViewController<iCarouselDataSource, iCarouselDelegate>
@property (strong, nonatomic) iCarousel *myCarousel;

_myCarousel = ({
        iCarousel *icarousel = [[iCarousel alloc] init];
        icarousel.dataSource = self;
        icarousel.delegate = self;
        icarousel.decelerationRate = 1.0;
        icarousel.scrollSpeed = 1.0;
        icarousel.type = iCarouselTypeLinear;
	icarousel.vertical = YES;				//默认为NO
        icarousel.pagingEnabled = YES;
        icarousel.clipsToBounds = YES;
        icarousel.bounceDistance = 0.2;
        [self.view addSubview:icarousel];
        [icarousel mas_makeConstraints:^(MASConstraintMaker *make) {
            make.edges.equalTo(self.view).insets(UIEdgeInsetsMake(44.0, 0, 0, 0));
        }];
        icarousel;
});
[self.view addSubview:_mySegmentControl];


@property (nonatomic, strong) NSMutableArray *items;

- (NSInteger)numberOfItemsInCarousel:(iCarousel *)carousel
	return items.count;

- (UIView *)carousel:(iCarousel *)carousel viewForItemAtIndex:(NSInteger)index reusingView:(UIView *)view
	if(view == nil)
		view = ]UIImageView alloc] initWithFrame:
		UILabel* label = [[UILabel alloc] init];
		label.tag = 1;
		[view addSubView:label];
	else
		UILabel* label = (UILabel*)[view withTag:1];

	return view;

- (void)carousel:(__unused iCarousel *)carousel didSelectItemAtIndex:(NSInteger)index
- (void)carouselCurrentItemIndexDidChange:(__unused iCarousel *)carousel
