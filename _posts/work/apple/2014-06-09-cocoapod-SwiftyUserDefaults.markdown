---
layout:     post
title:      "SwiftyUserDefaults"
subtitle:   " \"SwiftyUserDefaults\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
SwiftyUserDefaults
https://github.com/radex/SwiftyUserDefaults

install
pod ‘SwiftyUserDefaults'

import SwiftyUserDefaults



定义keys
extension DefaultsKeys {
    static let username = DefaultsKey<String?>("username")
    static let launchCount = DefaultsKey<Int>("launchCount")
}


use it
// Get and set user defaults easily
let username = Defaults[.username]
Defaults[.hotkeyEnabled] = true

// Modify value types in place
Defaults[.launchCount]++
Defaults[.volume] += 0.1
Defaults[.strings] += "… can easily be extended!"

// Use and modify typed arrays
Defaults[.libraries].append("SwiftyUserDefaults")
Defaults[.libraries][0] += " 2.0"

// Easily work with custom serialized types
Defaults[.color] = NSColor.whiteColor()
Defaults[.color]?.whiteComponent // => 1.0



let colorKey = DefaultsKey<String>(“color")
Defaults[colorKey] = “red"


