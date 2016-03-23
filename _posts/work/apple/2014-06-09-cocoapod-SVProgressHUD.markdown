---
layout:     post
title:      "SVProgressHUD"
subtitle:   " \"SVProgressHUD\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
SVProgressHUD
https://github.com/SVProgressHUD/SVProgressHUD

pod ‘SVProgressHUD'




//show 
+ (void)show;
(void)showWithStatus:(NSString*)string;

+ (void)showProgress:(CGFloat)progress;
(void)showProgress:(CGFloat)progress status:(NSString*)status;


//dismiss
+ (void)showProgress:(CGFloat)progress;
(void)showProgress:(CGFloat)progress status:(NSString*)status;

