---
layout:     post
title:      "Log"
subtitle:   " \"iOS Log\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
>[Log](https://github.com/delba/Log)
><small>目录:[cocoapod](/2014/06/09/cocoapod-cocoapod)</small>

```
extension Formatters {
    static let Detailed = Formatter("[%@] %@ - %@:%@ %@", [
        .Date("yyyy-MM-dd HH:mm:ss.SSS"),
        .File(fullPath: false, fileExtension: true),
        .Function,
        .Line,
//        .Level,
        .Message
        ])
}

extension Themes {
    static let TomorrowNight = Theme(
        trace:   "#C5C8C6",
        debug:   "#81A2BE",
        info:    "#B5BD68",
        warning: "#F0C674",
        error:   "#CC6666"
    )
}
let log = Logger(formatter: .Detailed, theme: .TomorrowNight)
log(object, use as print function)
```
