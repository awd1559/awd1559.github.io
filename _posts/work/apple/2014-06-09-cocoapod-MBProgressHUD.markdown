---
layout:     post
title:      "MBProgressHUD"
subtitle:   " \"MBProgressHUD\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
MBProgressHUD
https://github.com/jdg/MBProgressHUD

install
pod 'MBProgressHUD', '~> 0.9.2'







Usage

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


//swift
bridge.h
#import “MBProgressHUD/MBProgressHUD.h"
import MBProgressHUD

let hud = MBProgressHUD.showHUDAddedTo(self.view, animated:true)
hud.mode = MBProgressHUDMode.AnnularDeterminate
hud.labelText = "Loading"
hud.do