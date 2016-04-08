---
layout:     post
title:      "Masory"
subtitle:   " \"Masory\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
>[Masory](https://github.com/SnapKit/Masonry)
><small>目录:[cocoapod](/2014/06/09/cocoapod-cocoapod)</small>

pod "Masonry"

#import "Masonry.h"

#define kScreen_Bounds [UIScreen mainScreen].bounds
#define kScreen_Height [UIScreen mainScreen].bounds.size.height
#define kScreen_Width [UIScreen mainScreen].bounds.size.width
#define kScaleFrom_iPhone5_Desgin(_X_) (_X_ * (kScreen_Width/320))

view1 mas_makeConstraints:^(MASConstraintMaker *make){
	make.centerY.mas_equalTo(kScreen_Height/6);
}
[view2 mas_makeConstraints:^(MASConstraintMaker *make) {
        make.top.equalTo(view1.mas_bottom).offset(kScaleFrom_iPhone5_Desgin(45));
}];

make.left.greaterThanOrEqualTo(label);
make.left.greaterThanOrEqualTo(label.mas_left);
make.width.lessThanOrEqualTo(@400)
make.left.lessThanOrEqualTo(@10)

make.top.mas_equalTo(42);
make.height.mas_equalTo(20);
make.size.mas_equalTo(CGSizeMake(50, 100));
make.edges.mas_equalTo(UIEdgeInsetsMake(10, 0, 10, 0));
make.left.mas_equalTo(view).mas_offset(UIEdgeInsetsMake(10, 0, 10, 0));
