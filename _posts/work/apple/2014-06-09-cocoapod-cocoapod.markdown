---
layout:     post
title:      "cocoapod"
subtitle:   " \"cocoapod, list\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - Apple
---
# install

```
sudo gem install -g cocoapods
sudo gem uninsall cocoapods

pod setup    #设置环境

pod init          #创建一个Podfile文件
pod install
pod update
```

# make cocoapods

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


# 使用carthage
[carthage](/2014/06/09/cocoapod-carthage)


# 常用的pod
[awesome-iOS](https://github.com/vsouza/awesome-ios)
[awesome-iOS-ui](https://github.com/cjwirth/awesome-ios-ui)
[awesome-Swift](https://github.com/matteocrippa/awesome-swift)
[control preview](https://www.cocoacontrols.com/controls)


#### UI

- View
	[iCarousel](/2014/06/09/cocoapod-iCarousel)
	[SMPageControl](/2014/06/09/cocoapod-SMPageControl)
	[FXBlurView](/2014/06/09/cocoapod-FXBlurView)
	[ImageSlideshow](/2014/06/09/cocoapod-ImageSlideshow)
- Refresh
	[MJRefresh](/2014/06/09/cocoapod-MJRefresh)
	[ODRefreshControl](/2014/06/09/cocoapod-ODRefreshControl)
- autolayout
	[Masonry](/2014/06/09/cocoapod-Masonry)
	[Neon](/2014/06/09/cocoapod-Neon)
	[pureLayout](/2014/06/09/cocoapod-pureLayout)
	[SnapKit](/2014/06/09/cocoapod-SnapKit) 
	
	<small>用起来都不是很好，直接使用Storyboard，可以很好很直观的解决问题</small>
	<small>storyboard中还可以使用tab、nav、跳转</small>
- Layout
	[DrawerController](/2014/06/09/cocoapod-DrawerController)
	[PagingMenuController](/2014/06/09/cocoapod-PagingMenuController)
	[PageMenu](/2014/06/09/cocopod-PageMenu)
	[RESideMenu](/2014/06/09/cocoapod-RESideMenu)
	[XLPagerTabStrip](/2014/06/09/cocoapod-XLPagerTabStrip)
	[RDVTabBarController](/2014/06/09/cocoapod-RDVTabBarController)
	[RKSwipeBetweenViewControllers](/2014/06/09/cocoapod-RKSwipeBetweenViewControllers)
- HUD
	[MBProgressHUD](/2014/06/09/cocoapod-MBProgressHUD)
	[SVProgressHUD](/2014/06/09/cocoapod-SVProgressHUD)
	[PopMenu](/2014/06/09/cocoapod-PopMenu)
	[QuickDialog](/2014/06/09/cocoapod-QuickDialog)
	[JDStatusBarNotification](/2014/06/09/cocoapod-JDStatusBarNotification)
	
#### enhance
-
	[DateTools](/2014/06/09/cocoapod-DateTools)
	[SwiftyUserDefaults](/2014/06/09/cocoapod-SwiftyUserDefaults)
	[FontAwesome](/2014/06/09/cocoapod-FontAwesome)
	[AGEmojiKeyboard](/2014/06/09/cocoapod-AGEmojiKeyboard)
	
#### Reactive
-
	[RxSwift](/2014/06/09/cocoapod-RxSwift)
	[ReactiveCocoa](/2014/06/09/cocoapod-ReactiveCocoa)
	
#### Network
-
	[SDWebImage](/2014/06/09/cocoapod-SDWebImage)
	[AFNetworking](/2014/06/09/cocoapod-AFNetworking)
	[Alamofire](/2014/06/09/cocoapod-Alamofire)
	
#### Animation
-
	[Animo](/2014/06/09/cocoapod-animo)
	[pop](/2014/06/09/cocoapod-pop)
	
  - Introduction, Tutorials animation
	[JazzHands](/2014/06/09/cocoapod-JazzHands)
	[Presentation](https://github.com/hyperoslo/Presentation)
	
  - spring like animation lib
	[IBAnimatable](/2014/06/09/cocoapod-IBAnimatable)
	[Spring](/2014/06/09/cocoapod-spring)
	[Cheetah](https://github.com/suguru/Cheetah)
	[DKChainableAnimationKit](https://github.com/Draveness/DKChainableAnimationKit)
	[Morgan](https://github.com/RamonGilabert/Morgan)
	[Walker](https://github.com/RamonGilabert/Walker)
	
#### JSON
-
	[ObjectMapper](/2014/06/09/cocoapod-ObjectMapper)
	[SwiftyJSON](/2014/06/09/cocoapod-SwiftyJSON)
	
#### Xml
-
	[Ono](/2014/06/09/cocoapod-Ono)
	
#### Database
-
	[realmswift](/2014/06/09/cocoapod-realmswift)
	[FMDB](/2014/06/09/cocoapod-FMDB)
	
#### Log
-
	XCGLogger
	[log](2016/3/30/cocoapod-log)
	
	
#### misc

