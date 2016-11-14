---
layout:     post
title:      "ADT"
subtitle:   " \"Android Dev Tool\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - tools
---

*废弃*

# install

解压，指定sdk目录即可




# 混淆签名

> 使用混淆文件
> project.properties中加入proguard.config=proguard.txt

```
//生成keystore
keytool -genkey -alias android.keystore -keyalg RSA -validity 100000 -keystore android.keystore


Eclipse->File->Export->Export Android Application
->Select project
->Using the existing keystone, and input password
->select the destination APK file
```
