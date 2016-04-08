---
layout:     post
title:      "iCarousel"
subtitle:   " \"iCarousel,view旋转木马效果	\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
>[iCarousel](https://github.com/nicklockwood/iCarousel)
><small>目录:[cocoapod](/2014/06/09/cocoapod-cocoapod)</small>

# [iCarousel](https://github.com/nicklockwood/iCarousel)

#### install
only have two files: iCarousel.h、iCarousel.m

add QuartzCore
select project -> target -> build phases -> Link binary with Libraries


#### objective-c 
```
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
	icarousel.vertical = YES;				//NO by default
        icarousel.pagingEnabled = YES;
        icarousel.clipsToBounds = YES;
        icarousel.bounceDistance = 0.2;
        [self.view addSubview:icarousel];
        icarousel.frame = view.frame
        icarousel;
});
[self.view addSubview:_mySegmentControl];


@property (nonatomic, strong) NSMutableArray *items;

- (NSInteger)numberOfItemsInCarousel:(iCarousel *)carousel {
	return items.count;
}

- (UIView *)carousel:(iCarousel *)carousel viewForItemAtIndex:(NSInteger)index reusingView:(UIView *)view {
	if(view == nil)
		view = [UIImageView alloc] initWithFrame:
		UILabel* label = [[UILabel alloc] init];
		label.tag = 1;
		[view addSubView:label];
	else
		UILabel* label = (UILabel*)[view withTag:1];

	return view;
}

- (void)carousel:(__unused iCarousel *)carousel didSelectItemAtIndex:(NSInteger)index
- (void)carouselCurrentItemIndexDidChange:(__unused iCarousel *)carousel
```


#### swift

```
var carousel:iCarousel?
var items = ["1", "2", "3", "4", "5", "6", "7", "8", "9", "10", "11"]
```


```
carousel = iCarousel()
carousel!.frame = view.frame
carousel!.dataSource = self
carousel!.delegate = self
carousel!.decelerationRate = 1.0
carousel!.scrollSpeed = 1.0
carousel!.type = .Cylinder
carousel!.vertical = false
carousel!.pagingEnabled = true
carousel!.clipsToBounds = true
carousel!.bounceDistance = 0.2
view.addSubview(carousel!)
```

iCarouselDataSource
iCarouselDelegate

```
extension ViewController: iCarouselDataSource{
  func numberOfItemsInCarousel(carousel: iCarousel) -> Int {
    return items.count
  }
    
  func carousel(carousel: iCarousel, viewForItemAtIndex index: Int, reusingView view: UIView?) -> UIView {
    var result = view as? UIImageView
    var label = UILabel()
        
    if result == nil {
      result = UIImageView(frame: CGRect(x:0, y:0, width:200.0, height:200.0))
      result!.image = UIImage(named: "page")
      label.tag = 1
      result!.addSubview(label)
    } else {
      label = result!.viewWithTag(1) as! UILabel
    }
    label.text = items[index]
    
    return result!
  }
}

extension ViewController: iCarouselDelegate {
    
}
```


