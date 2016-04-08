---
layout:     post
title:      "XLPagerTabStrip"
subtitle:   " \"XLPagerTabStrip\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
>[XLPagerTabStrip](https://github.com/xmartlabs/XLPagerTabStrip)
><small>目录:[cocoapod](/2014/06/09/cocoapod-cocoapod)</small>

 
pod 'XLPagerTabStrip', '~> 4.0’

4种
Button Bar	:	ButtonBarPagerTabStripViewController 
Bar		:	BarPagerStripViewController
Twitter		:	TwitterPagerTabStripViewController
Segmented	:	SegmentedPagerTabStripViewController


import XLPagerTabStrip
class MyPagerTabStripName: ButtonBarPagerTabStripViewController{
	override public fund viewControllersForPagerTabStrip(pagerTabStripControllersForPagerTabStrip(pagerTabStripController: PagerTabStgripViewController) -> [UIViewController] {
		return [MyEmbeddedViewController(), MySecondEmbeddedViewController()]
	}

}

//必须 IndicatorInfoProvier 
class MyEmbeddedViewController: UITableViewController, IndicatorInfoProvider {

  func indicatorInfoForPagerTabStrip(pagerTabStripController: PagerTabStripViewController) -> IndicatorInfo {
    return IndicatorInfo(title: "My Child title")
  }
}

 

//定制




XLPagerTabStrip
https://github.com/xmartlabs/XLPagerTabStrip

//install
pod 'XLPagerTabStrip', '~> 4.0’

总共4种类型：
ButtonBar		ButtonBarPagerTabStripViewController
Bar			BarPagerTabStripViewController
Twitter			TwitterPagerTabStripViewController
Segmented		SegmentedPagerTabStripViewController


//使用
import XLPagerTabStrip

class MyPagerTabStripName: ButtonBarPagerTabStripViewController {
  override public func viewControllersForPagerTabStrip(pagerTabStripController: PagerTabStripViewController) -> [UIViewController] {
     return [MyEmbeddedViewController(), MySecondEmbeddedViewController()]
   }
}

class MyEmbeddedViewController: UITableViewController, IndicatorInfoProvider {
  func indicatorInfoForPagerTabStrip(pagerTabStripController: PagerTabStripViewController) -> IndicatorInfo {
    return IndicatorInfo(title: "My Child title”, image: UIImage(named:”home”))
   }
}


//自定义
public var pagerBehaviour: PagerTabStripBehaviour
override func viewDidLoad() {
	
	super.viewDidLoad() //必须放在最后，否则不起作用
}