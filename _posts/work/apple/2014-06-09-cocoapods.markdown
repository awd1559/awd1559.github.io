---
layout:     post
title:      "cocoapod"
subtitle:   " \"cocoapod, list\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
category: apple
permalink: /apple/cocoapods
tags:
    - Apple
---
><small>目录:[Apple目录](/apple/)</small>

> - 常用的pod
> - [awesome-iOS](https://github.com/vsouza/awesome-ios)
> - [awesome-iOS-ui](https://github.com/cjwirth/awesome-ios-ui)
> - [awesome-Swift](https://github.com/matteocrippa/awesome-swift)
> - [control preview](https://www.cocoacontrols.com/controls)


> - UI

#### pager


> - [PageMenu](https://github.com/HighBay/PageMenu)


```
let c1 = FirstViewController()
c1.title = ""
let c2 = SecondViewcontroller()
c2.title = ""
var controllers : [UIViewController] = [c1, c2]

var parameters: [CAPSPageMenuOption] = [
    .MenuItemSeparatorWidth(4.3), 
    .UseMenuLikeSegmentedControl(true), 
    .MenuItemSeparatorPercentageHeight(0.1)
]

var pageMenu = CAPSPageMenu(viewControllers: controllers, frame: CGRectMake(0.0, 0.0, self.view.frame.width, self.view.frame.height), pageMenuOptions: parameters)

self.view.addSubview(pageMenu!.view)
```





> - [PagingMenuController](https://github.com/kitasuke/PagingMenuController)


```
import PagingMenuController

//prepare controllers
let controller1 = First()
let controller2 = Second()
let viewControllers = [controller1, controller2]

//config options
let options = PagingMenuOptions()
options.menuItemMargin = 5
options.menuHeight = 60
options.menuDisplayMode = .SegmentedControl

//
let pagingMenuController = PagingMenuController(viewControllers: viewControllers, options: options)
pagingMenuController.view.frame.origin.y += 64
pagingMenuController.view.frame.size.height -= 64

addChildViewController(pagingMenuController)
view.addSubview(pagingMenuController.view)
pagingMenuController.didMoveToParentViewController(self)
```

> - use storyboard

```
let usersViewController = self.storyboard?.instantiateViewControllerWithIdentifier("UsersViewController") as! UsersViewController
let repositoriesViewController = self.storyboard?.instantiateViewControllerWithIdentifier("RepositoriesViewController") as! RepositoriesViewController

let viewControllers = [usersViewController, repositoriesViewController]

let options = PagingMenuOptions()
options.menuHeight = 50
   
let pagingMenuController = self.childViewControllers.first as! PagingMenuController
pagingMenuController.delegate = self
pagingMenuController.setup(viewControllers: viewControllers, options: options)
```






> - [XLPagerTabStrip](https://github.com/xmartlabs/XLPagerTabStrip)
> - 4种
> - Button Bar  :ButtonBarPagerTabStripViewController 
> - Bar         :BarPagerStripViewController
> - Twitter     :TwitterPagerTabStripViewController
> - Segmented   :SegmentedPagerTabStripViewController

```
class MyViewController: ButtonBarPagerTabStripViewController{
  override func viewDidLoad() {
    //xlpagertabstrip settings
    settings.style.buttonBarBackgroundColor = UIColor.red
    settings.style.buttonBarItemBackgroundColor = .clear
    settings.style.selectedBarBackgroundColor = UIColor(red: 234/255.0, green: 234/255.0, blue: 234/255.0, alpha: 1.0)
    settings.style.selectedBarHeight = 4.0
    settings.style.buttonBarMinimumLineSpacing = 0
    settings.style.buttonBarItemTitleColor = .black
    settings.style.buttonBarItemsShouldFillAvailableWidth = true
    settings.style.buttonBarLeftContentInset = 0
    settings.style.buttonBarRightContentInset = 0
    
    changeCurrentIndexProgressive = { (oldCell: ButtonBarViewCell?, newCell: ButtonBarViewCell?, progressPercentage: CGFloat, changeCurrentIndex: Bool, animated: Bool) -> Void in
        guard changeCurrentIndex == true else { return }
        oldCell?.label.textColor = UIColor(red: 138/255.0, green: 138/255.0, blue: 144/255.0, alpha: 1.0)
        newCell?.label.textColor = .white
    }

    super.viewDidLoad()
    navigationController?.navigationBar.shadowImage = UIImage()
    navigationController?.navigationBar.setBackgroundImage(UIImage(), for: .default)
  }

  override public func viewControllers(for pagerTabStripController: PagerTabStripViewController) -> [UIViewController] {
    return [First(), Second()]
  }
}


class First: UIViewController, IndicatorInfoProvider {
  func indicatorInfoForPagerTabStrip(pagerTabStripController: PagerTabStripViewController) -> IndicatorInfo {
    return IndicatorInfo(title: "My Child title”, image: UIImage(named:”home”))
   }
}
```






> - [RKSwipeBetweenViewControllers](https://github.com/cwRichardKim/RKSwipeBetweenViewControllers)

```
UIPageViewController *pageController = [[UIPageViewController alloc] initWithTransitionStyle:UIPageViewControllerTransitionStyleScroll   navigationOrientation:UIPageViewControllerNavigationOrientationHorizontal options:nil];
    
RKSwipeBetweenViewControllers *nav = [[RKSwipeBetweenViewControllers alloc]initWithRootViewController:pageController];

[nav.viewControllerArray addObjectsFromArray:@[ first, second, third]];
nav.buttonText = @[@"冒泡广场", @"朋友圈", @"热门冒泡"];
```


```
bridge.h
#import <RKSwipeBetweenViewControllers/RKSwipeBetweenViewControllers.h>

import RKSwipeBetweenViewControllers

let second = SecondViewController()
let third = ThirdViewController()
let four = FourViewController()

let pagerController = UIPageViewController(transitionStyle: .Scroll, navigationOrientation: .Horizontal, options: nil)
let nav = RKSwipeBetweenViewControllers(rootViewController: pagerController)
nav.viewControllerArray.addObjectsFromArray([second, third, four])
nav.buttonText = ["冒泡广场", "朋友圈", “热门冒泡"]
```











#### Tab



> - [RDVTabBarController](https://github.com/robbdimitrov/RDVTabBarController)

> - install

```
pod 'RDVTabBarController'
```

> - usage

```
TabBar
UIViewController* first = [[FirstViewController alloc]init];
UIViewController* second = [[SecondViewController alloc]init];
UIViewController* third = [[ThirdViewController alloc]init];

#import "RDVTabBarController.h"
RDVTabBarController* tab = [[RDVTabBarController alloc]init];
[tab setViewControllers:@[first, second, third]];
```



> - swift

```
bridge.h
#import “RDVTabBarController/RDVTabBarController.h"
#import “RDVTabBarController/RDVTabBarItem.h"

import RDVTabBarController
let first = FirstViewController()
let second = SecondViewController()
let tab = RDVTabBarController()
tab.viewControllers = [first, second]

//自定义
let tabImages = ["first", "second"]
for (idx, item) in tab.tabBar.items.enumerate() {
  let realItem = item as! RDVTabBarItem
  let image = UIImage(named: tabImages[idx])
  realItem.setFinishedSelectedImage(image, withFinishedUnselectedImage: image)
}

self.window.rootViewController = tab
```



> - 自定义

```
#import "RDVTabBarItem.h"
RDVTabBar* bar = [tab tabBar];
for (RDVTabBarItem *item in [bar items])
  item.titlePositionAdjustment = UIOffsetMake(-10, 5);
  [item setTitle:@""];
  [item setBadgeValue:@"1"];
  [item setBackgroundSelectedImage:backgroundImage withUnselectedImage:backgroundImage];
  [item setFinishedSelectedImage:selectedImage withFinishedUnselectedImage:unselectedImage];
```








> - [PageControls](https://github.com/popwarsweet/PageControls)
> - 4 styles
> - SnakePageControl
> - FilledPageControl
> - PillPageControl
> - ScrollingPageControl


```
let snakePageControl = SnakePageControl()
snakePageControl.pageCount = 3
snakePageControl.activeTint = .black
snakePageControl.inactiveTint = .white


snakePageControl.progress = progress
```











#### Slider


> - [ImageSlideshow](https://github.com/zvonicek/ImageSlideshow)

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












#### Refresh

> - [MJRefresh](https://github.com/CoderMJLee/MJRefresh)




> - [ODRefreshControl](https://github.com/Sephiroth87/ODRefreshControl)


```
#import "ODRefreshControl.h"

ODRefreshControl *refreshControl = [[ODRefreshControl alloc] initInScrollView:self.scrollView];

[refreshControl addTarget:self action:@selector(dropViewDidBeginRefreshing:) forControlEvents:UIControlEventValueChanged];

[refreshControl beginRefreshing];
[refreshControl endRefreshing];
```






#### autolayout


> - [SnapKit](https://github.com/SnapKit/SnapKit)


















> - [Masonry](https://github.com/SnapKit/Masonry)

```
pod 'Masonry'

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
```






> - [Cartography](https://github.com/robb/Cartography)
for swift


> - [FLKAutoLayout](https://github.com/floriankugler/FLKAutoLayout)
> - for Objective-C





#### Drawer

> - [DrawerController](https://github.com/sascha/DrawerController)

> -  install 

```
platform :ios, '8.0'
use_frameworks!

pod 'DrawerController', '~> 1.0'
```

> -  usage 

```
import DrawerController

//setup left and content controller
let centerNav = UINavigationController(rootViewController: HomeViewController())
let leftViewController = LeftViewController()
let rightViewController = RightViewController()

let drawerController = DrawerController(
  centerViewController: centerNav, 
  leftDrawerViewController: leftViewController,
  rightDrawerViewController: rightViewController)

drawerController.maximumLeftDrawerWidth=230
drawerController.maximumRightDrawerWidth=110
drawerController.openDrawerGestureModeMask=OpenDrawerGestureMode.PanningCenterView
drawerController.closeDrawerGestureModeMask=CloseDrawerGestureMode.All


self.window?.rootViewController = drawerController
```

> - in ViewController

```
//setup content controller navigation item
func setupNavigationItem(){
  let leftButton = NotificationMenuButton()
  leftButton.frame = CGRectMake(0, 0, 40, 40)
  self.navigationItem.leftBarButtonItem = UIBarButtonItem(customView: leftButton)
  leftButton.addTarget(self, action: Selector("leftClick"), forControlEvents: .TouchUpInside)
      
  let rightButton = UIButton(frame: CGRect(x:0, y:0, width:40, height:40))
  rightButton.contentMode = .Center
  rightButton.imageEdgeInsets = UIEdgeInsetsMake(0, 0, 0, -15)
  rightButton.setImage(UIImage.imageUsedTemplateMode("ic_more_horiz_36pt")!.imageWithRenderingMode(.AlwaysTemplate), forState: .Normal)
  self.navigationItem.rightBarButtonItem = UIBarButtonItem(customView: rightButton)
  rightButton.addTarget(self, action: Selector("rightClick"), forControlEvents: .TouchUpInside)
}
```

> - Selector

```
//get drawerController instance
func leftClick(){
	self.evo_drawerController?.toggleLeftDrawerSideAnimated(true, completion: nil)
}
func rightClick(){
	self.evo_drawerController?.toggleRightDrawerSideAnimated(true, completion: nil)
}

//get center view controller
self.evo_drawerController?.centerViewController
```






> - [RESideMenu](https://github.com/romaonthego/RESideMenu)













#### HUD


> - [MBProgressHUD](https://github.com/jdg/MBProgressHUD)

```
pod 'MBProgressHUD', '~> 0.9.2'
```


```
[MBProgressHUD showHUDAddedTo:self.view animated:YES];
dispatch_async(dispatch_get_global_queue( DISPATCH_QUEUE_PRIORITY_LOW, 0), ^{
    // Do something...
    dispatch_async(dispatch_get_main_queue(), ^{
        [MBProgressHUD hideHUDForView:self.view animated:YES];
    });
});




MBProgressHUD *hud = [MBProgressHUD showHUDAddedTo:self.view animated:YES];
hud.mode = MBProgressHUDModeAnnularDeterminate;
hud.labelText = @"Loading";
[self doSomethingInBackgroundWithProgressCallback:^(float progress) {
    hud.progress = progress;
} completionCallback:^{
    [hud hide:YES];
}];


[MBProgressHUD showHUDAddedTo:self.view animated:YES];
dispatch_time_t popTime = dispatch_time(DISPATCH_TIME_NOW, 0.01 * NSEC_PER_SEC);
dispatch_after(popTime, dispatch_get_main_queue(), ^(void){
    // Do something...
    [MBProgressHUD hideHUDForView:self.view animated:YES];
});




#import "MBProgressHUD.h"
MBProgressHUD *hud = [MBProgressHUD showHUDAddedTo:self.view animated:YES];
hud.mode = MBProgressHUDModeDeterminateHorizontalBar;
hud.labelText = @"Loading";
[self doSomethingInBackgroundWithProgressCallback:^(float progress) {
    hud.progress = progress;
} completionCallback:^{
    [hud hide:YES];
}];
```


> - swift

```
bridge.h
#import “MBProgressHUD/MBProgressHUD.h"
import MBProgressHUD

let hud = MBProgressHUD.showHUDAddedTo(self.view, animated:true)
hud.mode = MBProgressHUDMode.AnnularDeterminate
hud.labelText = "Loading"
hud.do
```









> - [SVProgressHUD](https://github.com/SVProgressHUD/SVProgressHUD)

> - install

```
pod 'SVProgressHUD'
```


> - usage

```
//config 
SVProgressHUD.setForegroundColor(UIColor(white: 1, alpha: 1))
SVProgressHUD.setBackgroundColor(UIColor(white: 0.15, alpha: 0.85))
SVProgressHUD.setDefaultMaskType(.None)

//show 
+ (void)show;
(void)showWithStatus:(NSString*)string;

+ (void)showProgress:(CGFloat)progress;
(void)showProgress:(CGFloat)progress status:(NSString*)status;


//dismiss
+ (void)showProgress:(CGFloat)progress;
(void)showProgress:(CGFloat)progress status:(NSString*)status;
```











#### Popup

> - [PopMenu](https://github.com/xhzengAIB/PopMenu)

```
pod 'PopMenu'
NSArray *items = @[
	[MenuItem itemWithTitle:@"项目" iconName:@"pop_Project" index:0],
        [MenuItem itemWithTitle:@"任务" iconName:@"pop_Task" index:1],
        [MenuItem itemWithTitle:@"冒泡" iconName:@"pop_Tweet" index:2],
        [MenuItem itemWithTitle:@"添加好友" iconName:@"pop_User" index:3],
        [MenuItem itemWithTitle:@"私信" iconName:@"pop_Message" index:4],
        [MenuItem itemWithTitle:@"两步验证" iconName:@"pop_2FA" index:5],
];
PopMenu *popMenu = [[PopMenu alloc] initWithFrame:self.view.bounds items:items];
popMenu.menuAnimationType = kPopMenuAnimationTypeNetEase; // kPopMenuAnimationTypeSina
popMenu.perRowItemCount = 3; // or 2
[popMenu showMenuAtView:self.view];

popMenu.didSelectedItemCompletion = ^(MenuItem *selectedItem) {
	switch(selectedItem.index)
}
```










#### Dialog

> - [QuickDialog](https://github.com/escoz/QuickDialog/)









#### misc


####[JDStatusBarNotification](https://github.com/jaydee3/JDStatusBarNotification)

> - install

```
pod 'JDStatusBarNotification'
```

> - usage

``` 
+ (JDStatusBarView*)showWithStatus:(NSString *)status;
+ (JDStatusBarView*)showWithStatus:(NSString *)status
                      dismissAfter:(NSTimeInterval)timeInterval;

+ (JDStatusBarView*)showWithStatus:(NSString *)status
                         styleName:(NSString*)styleName;

+ (JDStatusBarView*)showWithStatus:(NSString *)status
                      dismissAfter:(NSTimeInterval)timeInterval
                         styleName:(NSString*)styleName;

//关闭
+ (void)dismiss;
(void)dismissAfter:(NSTimeInterval)delay;
//显示进度
(void)showProgress:(CGFloat)progress;  // Range: 0.0 - 1.0

//active
+ (void)showActivityIndicator:(BOOL)show
               indicatorStyle:(UIActivityIndicatorViewStyle)style;


Animation Types
  • JDStatusBarAnimationTypeNone
  • JDStatusBarAnimationTypeMove
  • JDStatusBarAnimationTypeBounce
  • JDStatusBarAnimationTypeFade
Progress Bar Positions
  • JDStatusBarProgressBarPositionBottom
  • JDStatusBarProgressBarPositionCenter
  • JDStatusBarProgressBarPositionTop
  • JDStatusBarProgressBarPositionBelow
  • JDStatusBarProgressBarPositionNavBar


//swift
bridge.h
```

> - [iCarousel](https://github.com/nicklockwood/iCarousel)

> - install
> - only need two files: iCarousel.h、iCarousel.m
> - add QuartzCore
> - select project -> target -> build phases -> Link binary with Libraries


> - objective-c

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
  icarousel.vertical = YES;       //NO by default
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


> -  swift

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

> - iCarouselDataSource
> - iCarouselDelegate

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




	
# enhance

> -[ExSwift](https://github.com/pNre/ExSwift)


> - [DateTools](https://github.com/MatthewYork/DateTools)

```
let timeAgoDate = NSDate(timeIntervalSinceNow:-4)
timeAgoDate.timeAgoSinceNow
timeAgoDate.shortTimeAgoSinceNow


let date = NSDate()
let year: Int = date.year
let month  = date.month

let day = date.dayWithCalendar(calendar)


//日期比较
isEarlierThan
isEarlierThanOrEqualTo
isLaterThan
isLaterThanOrEqualTo
```




#### [Timepiece](https://github.com/naoty/Timepiece)
> - install

```
pod		pod “Timepiece"
```

> - usage 

```
let now = NSDate()
let nextWeek = now + 1.week
let dayAfterTomorrow = now + 2.days

// shortcuts #1
let today = NSDate.today()
let tomorrow = NSDate.tomorrow()
let yesterday = NSDate.yesterday()

// shortcuts #2
let dayBeforeYesterday = 2.days.ago
let tokyoOlympicYear = 5.years.later

//初始化
let birthday = NSDate.date(year: 1987, month: 6, day: 2)
let firstCommitDate = NSDate.date(year: 2014, month: 8, day: 15, hour: 20, minute: 25, second: 43)

let now = NSDate()
let christmas = now.change(month: 12, day: 25)
let thisSunday = now.change(weekday: 1)

// shortcuts
let newYearDay = now.beginningOfYear
let timeLimit = now.endOfHour


//Time Zone
let now = NSDate()
let cst = NSTimeZone(name: "CST")!
let dateInCST = now.beginningOfDay.change(timeZone: cst)
dateInCST.timeZone //=> CST (CDT) offset -18000 (Daylight)

//format and parse
5.minutes.later.stringFromFormat("yyyy-MM-dd HH:mm:SS")
//=> "2015-03-01 12:05:00"

"1987-06-02".dateFromFormat("yyyy-MM-dd")
//=> NSDate.date(year: 1987, month: 6, day: 2)
//比较
firstCommitDate < 1.year.ago // false
(1.year.ago...now).contains(firstCommitDate) // true
firstCommitDate > now // false
```







#### [SwiftyUserDefaults](https://github.com/radex/SwiftyUserDefaults)

> - install

```
pod 'SwiftyUserDefaults'
```

> - define

```
import SwiftyUserDefaults

//define default keys
extension DefaultsKeys {
  static let username = DefaultsKey<String?>("username")
  static let launchCount = DefaultsKey<Int>("launchCount")
  static let myarray = DefaultsKey<[String]>("myarray")
  static let myDictionary = DefaultsKey<[String: AnyObject]>("mydic")
}
```

> - usage

```
var username = Defaults[.username]
        
let nameKey = DefaultsKey<String>("color")
username = Defaults[nameKey]
        
Defaults[.launchCount] += 1
        
Defaults[.myarray].removeAll()
Defaults[.myarray].append("added into array")
Defaults[.myDictionary]["name"] = "aaa"
Defaults[.myarray][0] += "modified"
```












#### [FontAwesome.swift](https://github.com/thii/FontAwesome.swift)

> - install

```
use_frameworks!
pod ‘FontAwesome.swift'
```

> -  usage

```
import FontAwesome_swift//in label
label.font = UIFont.fontAwesomeOfSize(200)
label.text = String.fontAwesomeIconWithName(FontAwesome.Github)

//in label with code
label.font = UIFont.fontAwesomeOfSize(200)
label.text = String.fontAwesomeIconWithCode("fa-github")

//in button
button.titleLabel?.font = UIFont.fontAwesomeOfSize(30)
button.setTitle(String.fontAwesomeIconWithName(.Github), forState: .Normal)

//in navigation bar item
let attributes = [NSFontAttributeName: UIFont.fontAwesomeOfSize(20)] as Dictionary!
leftBarButton.setTitleTextAttributes(attributes, forState: .Normal)
leftBarButton.title = String.fontAwesomeIconWithName(.Github)

//toolbar item
let attributes = [NSFontAttributeName: UIFont.fontAwesomeOfSize(20)] as Dictionary!
toolbarItem.setTitleTextAttributes(attributes, forState: .Normal)
toolbarItem.title = String.fontAwesomeIconWithName(.Github)

//as image
tabBarItem.image = UIImage.fontAwesomeIconWithName(.Github, textColor: UIColor.blackColor(), size: CGSizeMake(30, 30))

//as image with background color
tabBarItem.image = UIImage.fontAwesomeIconWithName(FontAwesome.Github, textColor: UIColor.blueColor(), size: CGSizeMake(4000, 4000), backgroundColor: UIColor.redColor())
```













#### [AGEmojiKeyboard](https://github.com/ayushgoel/AGEmojiKeyboard)

> - install

```
pod "AGEmojiKeyboard"
```

> - Usage

```
#import "AGEmojiKeyboard.h"
AGEmojiKeyboardView *emojiKeyboardView = [[AGEmojiKeyboardView alloc] initWithFrame:CGRectMake(0, 0, self.view.frame.size.width, 216) dataSource:self];
emojiKeyboardView.autoresizingMask = UIViewAutoresizingFlexibleHeight;
emojiKeyboardView.delegate = self;
self.textView.inputView = emojiKeyboardView;


- (void)emojiKeyBoardView:(AGEmojiKeyboardView *)emojiKeyBoardView didUseEmoji:(NSString *)emoji {
  self.textView.text = [self.textView.text stringByAppendingString:emoji];
}

- (void)emojiKeyBoardViewDidPressBackSpace:(AGEmojiKeyboardView *)emojiKeyBoardView {

}
- (UIImage *)emojiKeyboardView:(AGEmojiKeyboardView *)emojiKeyboardView imageForSelectedCategory:(AGEmojiKeyboardViewCategoryImage)category {
  UIImage *img = [self randomImage];
  [img imageWithRenderingMode:UIImageRenderingModeAlwaysOriginal];
  return img;
}

- (UIImage *)emojiKeyboardView:(AGEmojiKeyboardView *)emojiKeyboardView imageForNonSelectedCategory:(AGEmojiKeyboardViewCategoryImage)category {
  UIImage *img = [self randomImage];
  [img imageWithRenderingMode:UIImageRenderingModeAlwaysOriginal];
  return img;
}

- (UIImage *)backSpaceButtonImageForEmojiKeyboardView:(AGEmojiKeyboardView *)emojiKeyboardView {
  UIImage *img = [self randomImage];
  [img imageWithRenderingMode:UIImageRenderingModeAlwaysOriginal];
  return img;
}
```


	
# Reactive


> - [RxSwift](https://github.com/ReactiveX/RxSwift)


> - [ReactiveCocoa](/2014/06/09/cocoapod-ReactiveCocoa)

# Image 

> - [SDWebImage](https://github.com/rs/SDWebImage)
> - Image downloader with cache




# Network

#### [Moya](https://github.com/Moya/Moya)


#### [AFNetworking](https://github.com/AFNetworking/AFNetworking)

> - install

```
platform :ios, '8.0'
pod 'AFNetworking', '~> 3.0'
```




#### [Alamofire](https://github.com/Alamofire/Alamofire)
> - swift Http library

> - install

```
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '10.0'
use_frameworks!

target '<Your Target Name>' do
    pod 'Alamofire', '~> 4.4'
end

```

> - usage


```
import Alamofire

Alamofire.request(.GET, “https://httpbin.org/get”).responseString{response in 
	self.label.text = response.result.value
}
```



> - 5 Response Handling

```
response
resonseData
responseString
responseJSON
responsePropertyList

request: NSURLRequest
response: NSHTTPURLResponse
data: NSData
error: NSError
```


> - response handler

```
Alamofire.request(.GET, "https://httpbin.org/get", parameters: ["foo": "bar"])
         .response { request, response, data, error in
             print(request)
             print(response)
             print(data)
             print(error)
          }
//response data handler
Alamofire.request(.GET, "https://httpbin.org/get", parameters: ["foo": "bar"])
         .responseData { response in
             print(response.request)
             print(response.response)
             print(response.result)
          }
//response string handler
Alamofire.request(.GET, "https://httpbin.org/get")
         .responseString { response in
             print("Success: \(response.result.isSuccess)")
             print("Response String: \(response.result.value)")
         } response json handler
Alamofire.request(.GET, "https://httpbin.org/get")
         .responseJSON { response in
             debugPrint(response)
         }
//chained response handlers
Alamofire.request(.GET, "https://httpbin.org/get")
         .responseString { response in
             print("Response String: \(response.result.value)")
         }
         .responseJSON { response in
             print("Response JSON: \(response.result.value)")
         }
```



> - xml handler
```
Alamofire.request(.POST, url, parameters: parameters).responseXMLDocument{ response in
    switch response.result {
    case .Success(let value):
        let result = value.root["result"]
        let errorCode = result["errorCode"].intValue
        let errorMessage = result["errorMessage"].stringValue
    case .Failure(let error):
        error.code
    }
}
```


> - HTTP methods

> - Parameters

> - HTTP Headers

```
let headers = [
    "Authorization": "Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==",
    "Content-Type": "application/x-www-form-urlencoded"
]

Alamofire.request(.GET, "https://httpbin.org/get", headers: headers)
         .responseJSON { response in
             debugPrint(response)
         }
```







# Animation

#### [Pop](https://github.com/facebook/pop)

```
PopBasicAnimation
PopSpringAnimation
PopDecayAnimation
PopCustomAnimation
```


> - Basic Usage

```
POPSpringAnimation *anim = [POPSpringAnimation animation];
[layer pop_addAnimation:anim forKey:@"myKey"];
[layer pop_removeAnimationForKey:@"myKey"];
anim = [layer pop_animationForKey:@"myKey"];
```



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
sender.layer.pop_addAnimation(decay, forKey: "fade")
```







```
// Common CALayer property names.
kPOPLayerBackgroundColor
kPOPLayerBounds
kPOPLayerCornerRadius
kPOPLayerBorderWidth
kPOPLayerBorderColor
kPOPLayerOpacity
kPOPLayerPosition
kPOPLayerPositionX
kPOPLayerPositionY
kPOPLayerRotation
kPOPLayerRotationX
kPOPLayerRotationY
kPOPLayerScaleX
kPOPLayerScaleXY
kPOPLayerScaleY
kPOPLayerSize
kPOPLayerSubscaleXY
kPOPLayerSubtranslationX
kPOPLayerSubtranslationXY
kPOPLayerSubtranslationY
kPOPLayerSubtranslationZ
kPOPLayerTranslationX
kPOPLayerTranslationXY
kPOPLayerTranslationY
kPOPLayerTranslationZ
kPOPLayerZPosition
kPOPLayerShadowColor
kPOPLayerShadowOffset
kPOPLayerShadowOpacity
kPOPLayerShadowRadius




// Common CAShapeLayer property names.
kPOPShapeLayerStrokeStart
kPOPShapeLayerStrokeEnd
kPOPShapeLayerStrokeColor
kPOPShapeLayerFillColor
kPOPShapeLayerLineWidth
kPOPShapeLayerLineDashPhase



// Common NSLayoutConstraint property names.
kPOPLayoutConstraintConstant



// Common UIView property names.
kPOPViewAlpha
kPOPViewBackgroundColor
kPOPViewBounds
kPOPViewCenter
kPOPViewFrame
kPOPViewScaleX
kPOPViewScaleXY
kPOPViewScaleY
kPOPViewSize
kPOPViewTintColor



// Common UIScrollView property names.
kPOPScrollViewContentOffset
kPOPScrollViewContentSize
kPOPScrollViewZoomScale
kPOPScrollViewContentInset
kPOPScrollViewScrollIndicatorInsets



// Common UITableView property names.
kPOPTableViewContentOffset
kPOPTableViewContentSize



// Common UICollectionView property names.
kPOPCollectionViewContentOffset
kPOPCollectionViewContentSize



// Common UINavigationBar property names.
kPOPNavigationBarBarTintColor



// Common UIToolbar property names.
kPOPToolbarBarTintColor



// Common UITabBar property names.
kPOPTabBarBarTintColor



// Common UILabel property names.
kPOPLabelTextColor
```



> - [Spring](https://github.com/MengTo/Spring)
> - swift 
> - shark, pull etc.











> - [Hero](https://github.com/lkzhao/Hero)
> - Elegant transition library for iOS & tvOS









#### Introduction, Tutorials animation

> - [JazzHands](/2014/06/09/cocoapod-JazzHands)
> - for Objective-C




> - 4个步骤
> - 1、继承IFTTTAnimatedPagingScrollViewController
> - 2、创建view，到contentView
> - 3、设定view是在哪个page上
> - 4、为view设定动画




```
bridege.h
#include "JazzHands/IFTTTJazzHands.h"

import JazzHands

class ViewController : IFTTTAnimatedPagingScrollViewController

override func numberOfPages() -> UInt {
  return 4
}

override func viewDidLoad() {
  super.viewDidLoad()

  //create view, and added to contentView
  let imageview0 = UIImageView(image: UIImage(named:""))
  self.contentView.addSubview(imageview0)

  //keep view on certain pages
  self.keepView(imageview0, onPage:0)     //show imageview0 on page0
  self.keepView(imageview2, onPages:[2,3])  //show imageview2 on page2 & page3
  
  //create animations
  let alphaAnimation = IFTTTAlphaAnimation(view:view_you_want_to_animate)
  alphaAnimation.addKeyframeForTime(30, alpha:1.0)
  alphaAnimation.addKeyframeForTime(60, alpha:0.0)

  //add animator
  self.animator = IFTTTAnimator()
  self.animator.addAnimation(alphaAnimation)
}
```







> - [RazzleDazzle](https://github.com/IFTTT/RazzleDazzle)
> - for swift



> - [Presentation](https://github.com/hyperoslo/Presentation)

> - [Cheetah](https://github.com/suguru/Cheetah)

> - [DKChainableAnimationKit](https://github.com/Draveness/DKChainableAnimationKit)

> - [Morgan](https://github.com/RamonGilabert/Morgan)

> - [Walker](https://github.com/RamonGilabert/Walker)















# Database


> - [RealmSwift](https://github.com/realm/realm-cocoa)

> - install

```
pod 'RealmSwift'
```


> - doc

```
https://realm.io/docs/swift/latest/
```








> - [FMDB](https://github.com/ccgus/fmdb)

> - install

```
pod 'FMDB'
```

> - FMDatabase
> - FMResultSet
> - FMDatabaseQueue

```
//存在打开，不存在则创建
//@"": 在临时文件夹创建空数据库
//NULL: 内存数据库
FMDatabase *db = [FMDatabase databaseWithPath:@"/tmp/tmp.db"];

if (![db open]) {
    [db release];
    return;
}
NSString *sql = @"CREATE TABLE 'User' ('id' INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL, 'name' VARCHAR(30), 'password' VARCHAR(30)) ";
BOOL res = db executeUpdate:sql
if (!res)

//query
FMResultSet *rs = [db executeQuery:@"SELECT * FROM myTable"];
while ([rs next]) {
  NSNumber* id = [NSNumber numberWithInt:[rs intForColumnIndex:0]];
  NSString* name = [rs stringForColumn:@"name"];
  
  const unsigned char* ccchar = [rs UTF8StringForColumnName:@"chinesename"];
  NSString* cname = [[NSString alloc] initWithCString:ccchar encoding:NSUTF8StringEncoding];
  
  NSData* avata = [rs dataForColumn:@"avata"];
}

FMResultSet *rs = [db executeQuery:@"SELECT COUNT(*) FROM myTable"];
if ([s next]) {
    int totalCount = [s intForColumnIndex:0];
    NSString *pass = [s stringForColumn:@“name”];
}
[rs close];
[db close];




NSString* docsdir = [NSSearchPathForDirectoriesInDomains( NSDocumentDirectory, NSUserDomainMask, YES) lastObject];
NSString* dbpath = [docsdir stringByAppendingPathComponent:@"user.sqlite"];
FMDatabase* db = [FMDatabase databaseWithPath:dbpath];
[db open];
FMResultSet *rs = [db executeQuery:@"select * from people"];
while ([rs next]) {
    NSLog(@"%@ %@",
        [rs stringForColumn:@"firstname"],
        [rs stringForColumn:@"lastname"]);
}
[db close];
```







# model

> - [Mantle](https://github.com/Mantle/Mantle)
> - model framework

> - [Argo](https://github.com/thoughtbot/Argo)


> - [SwiftyJSON](https://github.com/SwiftyJSON/SwiftyJSON)


```
let url = "https://api.github.com/users/octocat/repos"
Alamofire.request(url).responseJSON{ response in
  switch response.result {
    case .success:
      let json = JSON(data: response.data!)
      
      for item in json.array! {
          print(item["name"])
      }
      self.label.text = json[0, "full_name"].string
    case .failure(let error):
      print(error)
  }
}
```


> - [AlamofireJsonToObjects](https://github.com/evermeer/AlamofireJsonToObjects)

```
import AlamofireJsonToObjects

import Foundation
import EVReflection
class User:EVObject{
    var id = ""
    var name = ""
    var full_name = ""
    var owner: Owner = Owner()
}
class Owner:EVObject {
    var login = ""
    var id = ""
    var avatar_url = ""
}



let url = "https://api.github.com/users/octocat/repos"
Alamofire.request(url).responseArray{(response: DataResponse<[User]>) -> Void in
  switch response.result {
  case .success:
      for user in response.value! {
          print(user.name + ": " + user.owner.login)
      }
  case .failure(let error):
      print(error)
  }
}
```


> - [ObjectMapper](https://github.com/Hearst-DD/ObjectMapper)


```
class User: Mappable {
    var username: String?
    var age: Int?
    var weight: Double!
    var array: [AnyObject]?
    var dictionary: [String : AnyObject] = [:]
    var bestFriend: User?                       // Nested User object
    var friends: [User]?                        // Array of Users
    var birthday: NSDate?

    required init?(_ map: Map) {

    }

    // Mappable
    func mapping(map: Map) {
        username      <- map["username"]
        age             <- map["age"]
        weight        <- map["weight"]
        array           <- map["arr"]
        dictionary    <- map["dict"]
        bestFriend    <- map["best_friend"]
        friends       <- map["friends"]
        birthday      <- (map["birthday"], DateTransform())
    }
}


//JSONString -> model
let user = Mapper<User>().map(JSONString)
//Model -> JSONString
let JSONString = Mapper().toJSONString(user, prettyPrint: true)



//嵌套
"distance" : {
     "text" : "102 ft",
     "value" : 31
}

func mapping(map: Map) {
    distance <- map["distance.value"]
}
distance <- map["distances.0.value"]
```




> - [Ono](https://github.com/mattt/Ono)






	
# Log

> - [Log](https://github.com/delba/Log)

```
extension Formatters {
    static let Detailed = Formatter("[%@] %@ - %@:%@ %@", [
        .Date("yyyy-MM-dd HH:mm:ss.SSS"),
        .File(fullPath: false, fileExtension: true),
        .Function,
        .Line,
//        .Level,
        .Message
        ])
}

extension Themes {
    static let TomorrowNight = Theme(
        trace:   "#C5C8C6",
        debug:   "#81A2BE",
        info:    "#B5BD68",
        warning: "#F0C674",
        error:   "#CC6666"
    )
}
let log = Logger(formatter: .Detailed, theme: .TomorrowNight)
log(object, use as print function)
```



	
# misc

> - [SwiftyBeaver](https://github.com/SwiftyBeaver/SwiftyBeaver)


> - [FXBlurView](https://github.com/nicklockwood/FXBlurView)
> - on iOS 5 and above

```
pod 'FXBlurView', '~> 1.6.4'

//only have two files: FXBlurView.h, FXBlurView.m
```

> - usage

```
import FXBlurView

//set background
let frostedView = FXBlurView()
frostedView.underlyingView = UIImageView(image:UIImage(named:"nemo"))
frostedView.isDynamic = false
frostedView.tintColor = UIColor.black
frostedView.frame = CGRect(x:0.0, y:view.frame.height/2, width:view.frame.width, height:view.frame.height/2)
view.addSubview(frostedView)

//show someview on top
let someview = UIView()
someview.frame = frostedView.frame
view.addSubview(someview)
```








> - [SMPageControl](https://github.com/Spaceman-Labs/SMPageControl)

```
@property (strong, nonatomic) SMPageControl *pageControl;

self.pageControl = ({
  SMPageControl *pageControl = [[SMPageControl alloc] init];
  pageControl.numberOfPages = self.numberOfPages;
  pageControl.userInteractionEnabled = NO;
  pageControl.pageIndicatorImage = pageIndicatorImage;
  pageControl.currentPageIndicatorImage = currentPageIndicatorImage;
  [pageControl sizeToFit];
  pageControl.currentPage = 0;
  pageControl;
});
[self.view addSubview:self.pageControl];
```












#### cocoapods
> - install

```
brew install cocoapods

sudo gem install -g cocoapods
sudo gem uninsall cocoapods

pod setup    #设置环境

pod init          #创建一个Podfile文件
pod install
pod update
```

> - make cocoapods

```
pod trunk register awd1559@gmail.com 'awd1559' //注册

//生成SwiftyExt.podspec
pod spec create NAME
//检查
pod spec lint SwiftyExt.podspec  
//添加到本地repo spec
pod repo push SPECNAME NAME.podspec

修改SwiftyExt.podspec版本
git tag '1.1.1'
git push --tags
//删除原称tag
git push origin —delete tag <tagnaem>  

//上传到cocoapods
pod trunk push SwiftyExt.podspec  
```


#### Cartfile

```
brew install Carthage
brew upgrade Carthage

carthage version
carhage update
```


