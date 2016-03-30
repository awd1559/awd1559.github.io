---
layout:     post
title:      "DateTools"
subtitle:   " \"DateTools\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
[DateTools](https://github.com/MatthewYork/DateTools)


# install

```
pod 'DateTools'
```

# usage

```
let timeAgoDate = NSDate(timeIntervalSinceNow:-4)
timeAgoDate.timeAgoSinceNow
timeAgoDate.shortTimeAgoSinceNow


let date = NSDate()
let year: Int = date.year
let month  = date.month

let day = date.dayWithCalendar(calendar)
```

//日期比较
isEarlierThan
isEarlierThanOrEqualTo
isLaterThan
isLaterThanOrEqualTo


参考Timepiece

对于Swift，Timepiece更方便
[Timepiece](https://github.com/naoty/Timepiece)

# install

```
pod		pod “Timepiece"
```

# usage 

```
let now = NSDate()
let nextWeek = now + 1.week
let dayAfterTomorrow = now + 2.days

// shortcuts #1
let today = NSDate.today()
let tomorrow = NSDate.tomorrow()
let yesterday = NSDate.yesterday()

// shortcuts #2
let dayBeforeYesterday = 2.days.ago
let tokyoOlympicYear = 5.years.later

//初始化
let birthday = NSDate.date(year: 1987, month: 6, day: 2)
let firstCommitDate = NSDate.date(year: 2014, month: 8, day: 15, hour: 20, minute: 25, second: 43)

let now = NSDate()
let christmas = now.change(month: 12, day: 25)
let thisSunday = now.change(weekday: 1)

// shortcuts
let newYearDay = now.beginningOfYear
let timeLimit = now.endOfHour


//Time Zone
let now = NSDate()
let cst = NSTimeZone(name: "CST")!
let dateInCST = now.beginningOfDay.change(timeZone: cst)
dateInCST.timeZone //=> CST (CDT) offset -18000 (Daylight)

//format and parse
5.minutes.later.stringFromFormat("yyyy-MM-dd HH:mm:SS")
//=> "2015-03-01 12:05:00"

"1987-06-02".dateFromFormat("yyyy-MM-dd")
//=> NSDate.date(year: 1987, month: 6, day: 2)
//比较
firstCommitDate < 1.year.ago // false
(1.year.ago...now).contains(firstCommitDate) // true
firstCommitDate > now // false
```
