---
layout:     post
title:      "ai"
subtitle:   " \"常用方法和快捷键\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - tools
---
ADT
解压，指定sdk目录即可
需要添加项目appcompat_v7为android lib，才可以编译，appcompat_v7项目用ADT新建项目自动生成一个


minSdkVersion/maxSdkVersion:在安装时限制可安装设备
targetSdkVersion:程序运行时起作用


混淆签名
使用混淆文件
project.properties中加入proguard.config=proguard.txt
生成keystore
keytool -genkey -alias android.keystore -keyalg RSA -validity 100000 -keystore android.keystore
Eclipse->File->Export->Export Android Application->Select project
->Using the existing keystone, and input password->select the destination APK file








