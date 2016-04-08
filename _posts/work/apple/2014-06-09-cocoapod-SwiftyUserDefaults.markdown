---
layout:     post
title:      "SwiftyUserDefaults"
subtitle:   " \"SwiftyUserDefaults\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
>[SwiftyUserDefaults](https://github.com/radex/SwiftyUserDefaults)
><small>目录:[cocoapod](/2014/06/09/cocoapod-cocoapod)</small>

# install
```
pod 'SwiftyUserDefaults'
```

# define
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

# usage
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
