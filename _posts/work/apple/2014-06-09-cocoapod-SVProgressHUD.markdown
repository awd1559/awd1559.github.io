---
layout:     post
title:      "SVProgressHUD"
subtitle:   " \"SVProgressHUD\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
>[SVProgressHUD](https://github.com/SVProgressHUD/SVProgressHUD)
><small>目录:[cocoapod](/2014/06/09/cocoapod-cocoapod)</small>

# install

```
pod ‘SVProgressHUD'
```


# usage

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
