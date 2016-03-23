---
layout:     post
title:      "Alamofire"
subtitle:   " \"Alamofire\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
```swift
- (void)viewDidLoad
{
    [super viewDidLoad];

    UIImageView *iv = [[UIImageView alloc] initWithImage:nil];
    iv.contentMode = UIViewContentModeScaleAspectFit;
    // Do not produce a translated constraint for this view
    iv.translatesAutoresizingMaskIntoConstraints = NO;

    [self.view addSubview:iv];

    NSDictionary *nameMap = @{@"imageView": self.imageView,
                              @"dateLabel": self.dateLabel,
                              @"toolbar": self.toolbar};

    // imageView is 0 pts from superview at left and right edges
    NSArray *horizontalConstraints =
        [NSLayoutConstraint constraintsWithVisualFormat:@"H:|-0-[imageView]-0-|"
                                                options:0
                                                metrics:nil
                                                  views:nameMap];

    // imaveView is 8 pts from dateLabel at its top edge...
    // ... and 8 pts from toolbar at its bottom edge
    NSArray *verticalConstraints =
        [NSLayoutConstraint constraintsWithVisualFormat:@"V:[dateLabel]-[imageView]-[toolbar]"
                                                options:0
                                                metrics:nil
                                                  views:nameMap];

    [self.view addConstraints:horizontalConstraints];
    [self.view addConstraints:verticalConstraints];
}
AutoLayoutConstraints

VFL
NSDictionary *nameMap = @{@"imageView": self.imageView,
                              @"dateLabel": self.dateLabel,
                              @"toolbar": self.toolbar};
NSArray *horizontalConstraints = [NSLayoutConstraint constraintsWithVisualFormat:@"H:|-0-[imageView]-0-|"
                                                options:0
                                                metrics:nil
                                                views:nameMap];
NSArray *verticalConstraints = [NSLayoutConstraint constraintsWithVisualFormat:@"V:[dateLabel]-[imageView]-[toolbar]"
                                                options:0
                                                metrics:nil
                                                views:nameMap];

[self.view addConstraints:horizontalConstraints];
[self.view addConstraints:verticalConstraints];
```

手动添加Constraint
[self.view addConstraint: [NSLayoutConstraint constraintWithItem:blueView           blueview left = redview left * 1 + 0
attribute:NSLayoutAttributeLeft
relatedBy:NSLayoutRelationEqual
toItem:redView
attribute:NSLayoutAttributeLeft
multiplier:1
constant:0]];

如果UI布局不变，只有在不同屏幕尺寸上有适应性变化，需要自动拉伸和位移，就要添加constraints
约束冲突，使用优先级
