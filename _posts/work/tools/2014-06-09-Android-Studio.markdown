---
layout:     post
title:      "Android Studio"
subtitle:   " \"常用方法和快捷键\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - tools
---

# error fix

first run, show 'Fetching Android component iniformation' failed

open studio/bin/idea.properties
```
disable.android.first.run=true
```

# keymap
- symbols: cmd+shit+o
- structure: cmd+7 (like outline in eclipse)
- nav backward: cmd+[
- nav forward:  cmd+]
- run        :  cmd+r
- setting : cmd+,
- search everywhere: double shift

# menu 
- Theme：Appearance—>Theme->Darcula
- Font：Editor—>Color & Font —> Size —> 16
- Encoding：File Encodings—>
- Line Number：Editor—>Appearance—>Show Line numbers
- Tab：Editor—>Appearance—>Show whitespaces
- auto import：Editor—>Auto import add unambiguous imports on the fly
- spelling check：Editor->Inspections—>Spelling
- git：Version Control—>Git
- Plugins：Plugins

导入第三方库：
import module
修改build.gradle中相对应的版本参数

问题：
Failed to resolve: com.android.support:appcompat-v7:21.+
是sdk不完整造成的，更新sdk，修改到19.+

asset
src/main/asset/
xxx.imi中添加：
	<option Name=








minSdkVersion/maxSdkVersion:在安装时限制可安装设备
targetSdkVersion:程序运行时起作用





# ADT->Android Studio

> - ADT版本必须在22及以上
> - Eclipse工程—>Export->Generate Gradle Build Files
> - 生成build.gradle文件
> - Launch Android Stuidio
> - Import Project







使用EmptyActivity创建，可避免content_main.xml等layout文件





