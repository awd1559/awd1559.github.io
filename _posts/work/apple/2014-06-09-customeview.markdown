---
layout:     post
title:      "customview"
subtitle:   " \"customview\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - iOS
---
# 自定义view
```
//MyUIView : UIView
- (id)initWithFrame:(CGRect)frame
{
    self = [super initWithFrame:frame];
    if (self) {
        self.backgroundColor = [UIColor clearColor];
    }
    return self;
}

- (void)drawRect:(CGRect)rect
{
    CGRect bounds = self.bounds;

    CGPoint center;
    center.x = bounds.origin.x + bounds.size.width / 2.0;
    center.y = bounds.origin.y + bounds.size.height / 2.0;

    float maxRadius = hypot(bounds.size.width, bounds.size.height) / 2.0;

    UIBezierPath *path = [[UIBezierPath alloc] init];

    for (float currentRadius = maxRadius; currentRadius > 0; currentRadius -= 20) {
        [path moveToPoint:CGPointMake(center.x + currentRadius, center.y)];

        [path addArcWithCenter:center
                        radius:currentRadius
                    startAngle:0.0
                      endAngle:M_PI * 2.0
                     clockwise:YES];
    }

    // Configure line width to 10 points
    path.lineWidth = 10;

    // Configure the drawing color to light gray
    [[UIColor lightGrayColor] setStroke];

    // Draw the line!
    [path stroke];
}
```




```
//自定义view
view中包涵内部action
新建MyView : UIView
+(UIView*)instanceOfMyView
{
	NSArray* nibView =  [[NSBundle mainBundle] loadNibNamed:@"MyView" owner:nil options:nil];
        return [nibView objectAtIndex:0];
}
```

```
创建MyView.xib
拖动IBAction， IBOutlet


在ViewController中
UIView* view = [MyView instanceOfMyView];
view.frame = CGRectMake(100, 200, 400, 400);
[self.view addSubview:view];


问题：屏幕对齐等使用layout constraints 约束
```
