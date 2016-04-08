---
layout:     post
title:      "Spring"
subtitle:   " \"Animation\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
>[Spring](https://github.com/MengTo/Spring)
><small>目录:[cocoapod](/2014/06/09/cocoapod-cocoapod)</small>


# install
```
use_frameworks!
pod 'Spring', :git => 'https://github.com/MengTo/Spring.git', :branch => 'swift2'
```

# usage
```
let button = SpringButton()
button.animation = Spring.AnimationPreset.Shake.rawValue
button.animate()

SpringView
SpringButton
SpringImageView
SpringLabel
SpringTextField
SpringTextView
```

