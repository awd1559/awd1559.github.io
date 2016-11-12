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
Android Studio keng
先运行一次，启动时出现Fetching Android component iniformation
不一定会获取成功
打开studio/bin目录idea.properties
最后一行添加disable.android.first.run=true


keymap:
symbols: cmd+shit+o
structure: cmd+7 (like outline in eclipse)
nav backward: cmd+[
nav forward:  cmd+]
run        :  cmd+r

设置
Command+,
主题：Appearance—>Theme->Darcula
字体：Editor—>Color & Font —> Size —> 16
编码：File Encodings—>
行号：Editor—>Appearance—>Show Line numbers
Tab和空格：Editor—>Appearance—>Show whitespaces
自动import：Editor—>Auto import add unambiguous imports on the fly
拼音检查：Editor->Inspections—>Spelling
版本控制：Version Control—>Git
插件：Plugins

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





从ADT导入工程到Android Studio
ADT版本必须在22及以上
Eclipse工程—>Export->Generate Gradle Build Files
生成build.gradle文件
Android Stuidio
Import Project
################################################################









使用EmptyActivity创建，可避免content_main.xml等layout文件

double shift : search everywhere
