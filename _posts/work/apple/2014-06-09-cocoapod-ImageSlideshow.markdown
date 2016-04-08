---
layout:     post
title:      "ImageSlideshow"
subtitle:   " \"ImageSlideshow\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
>[ImageSlideshow](https://github.com/zvonicek/ImageSlideshow)
><small>目录:[cocoapod](/2014/06/09/cocoapod-cocoapod)</small>

```
let slideshow = ImageSlideshow()
slideshow.frame = CGRect(x:0, y:0, width: view.frame.width, height: view.frame.height/2)

slideshow.backgroundColor = UIColor.whiteColor()
slideshow.slideshowInterval = 5.0
slideshow.pageControlPosition = .InsideScrollView      //Hidden
slideshow.pageControl.currentPageIndicatorTintColor = UIColor.lightGrayColor()
slideshow.pageControl.pageIndicatorTintColor = UIColor.blackColor()

slideshow.setImageInputs([ImageSource(imageString: "img1")!, ImageSource(imageString: "img2")!, ImageSource(imageString: "img3")!, ImageSource(imageString: "img4")!])

view.addSubview(slideshow)
```

```
let recognizer = UITapGestureRecognizer(target: self, action: "click")
slideshow.addGestureRecognizer(recognizer)

var transitionDelegate: ZoomAnimatedTransitioningDelegate?  //no use
func click() {
  let ctr = FullScreenSlideshowViewController()
  ctr.pageSelected = {(page: Int) in
    self.slideshow.setScrollViewPage(page, animated: false)
  }

  ctr.initialPage = slideshow.scrollViewPage
  ctr.inputs = slideshow.images
  self.transitionDelegate = ZoomAnimatedTransitioningDelegate(slideshowView: slideshow);
  ctr.transitioningDelegate = self.transitionDelegate!
  self.presentViewController(ctr, animated: true, completion: nil)
}
```


