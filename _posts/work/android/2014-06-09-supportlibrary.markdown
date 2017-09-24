---
layout:     post
title:      "Android Support Library"
subtitle:   " \"Android Support Library\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
category: android
permalink: /android/support
tags:
    - Android
---
><small>目录:[Android目录](/android/)</small>


```
final SUPPORT_LIBRARY_VERSION = '25.2.0'

compile 'com.android.support:support-v4:*'
compile 'com.android.support:support-compat:*'
compile 'com.android.support:support-core-ui:26.+'
compile 'com.android.support:support-fragment:26.+'

compile 'com.android.support:multidex:1.0.1'

compile 'com.android.support:appcompat-v7:26.+'
compile 'com.adnroid.support:cardview-v7:26.+'
compile 'com.android.support:recyclerview-v7:26.+'
compile 'com.android.support:design:26.+'
compile 'com.android.support:percent:26.+'
compile 'com.android.support:preference-v7:26.+'


compile 'com.android.support:customtabs:${supportLibVersion}'
compile 'com.android.support.constraint:constraint-layout:1.0.2'
compile 'com.android.support:support-annotations:${supportLibVersion}'
```






```
//test
android {
    defaultConfig {
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
    }
}
dependencies {
  androidTestCompile 'com.android.support.test:runner:0.4'
  // Set this dependency to use JUnit 4 rules
  androidTestCompile 'com.android.support.test:rules:0.4'
  // Set this dependency to build and run Espresso tests
  androidTestCompile 'com.android.support.test.espresso:espresso-core:2.2.1'
  // Set this dependency to build and run UI Automator tests
  androidTestCompile 'com.android.support.test.uiautomator:uiautomator-v18:2.1.2'
}
```