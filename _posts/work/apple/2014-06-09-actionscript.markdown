---
layout:     post
title:      "Apple Action Script"
subtitle:   " \"apple action script\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
category: apple
permalink: /apple/actionscript
tags:
    - Apple
---
><small>目录:[Apple目录](/apple/)</small>


# AppleScript

> - 利用AppleScript实现流程自动化
> - 不要求大小写
> - 一旦发现错误，后面的内容不再执行

> - 注释

```
#
-
(**)
```

```
beep    
beep 2
say “this is a spoken s” using “Zarvox”
say “hello” & “ morning”

tell application “Finder”
    empty the trash
    open the startup disk
end tell

display dialog “”                   #显示dialog
display dialog “” buttons {“OK”}            #按钮
display dialog “string” buttons {}  default button 3    #默认第三个button 

set x to 25
set y to 4321.222
set pictureWidth to 8
set the second item of myList to “value”
set the 2nd item of myList to “spring”
set myValueOfLastItem to the last item of myList
set myValueOfLastItem to item-1 of myList
set myRange to items 2 through 5 of myList      #index从1开始计算
set myRange to items 5 through 2 of myList
set myValue to reverse of myList
set myLen  to the length of myList
set x to some item of myList            #随机
set myValue to every character of myString
set person to {age:5, name:”awd”}
set temp to the age of person
set myName to display dialog “who are you?” default answer “awd”
say “hello “ & text returned of myName


if true then
end if

if false then 
end if

if myString begins with “what” then ……                 #begins with, ends with, starts with
if myString does not start with “what” then ……  #is equal to 
if myString contains “what” then ……     #comes before, comes after, is in, contains
does not 
is not

considering case
    …… #这里考虑字母大小写
end considering

ignoring white space
    …… #这里忽略空格、换行、制表符
end ignoring
```