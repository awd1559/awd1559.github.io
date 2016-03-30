---
layout:     post
title:      "persistence"
subtitle:   " \"persistence\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - iOS
---
文件

NSArray* documentDirectory = NSSearchPathForDirectoriesInDomains (NSDocumentDirectory, NSUserDomainMask, YES);
NSArray* libraryDirectory       = NSSearchPathForDirectoriesInDomains (NSLibraryDirectory,       NSUserDomainMask, YES);
NSString* tmpDirectory          = NSTemporaryDirectory();


属性列表









