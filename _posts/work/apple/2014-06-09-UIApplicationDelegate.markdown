---
layout:     post
title:      "UIApplicationDelegate"
subtitle:   " \"application delegate\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - iOS
---
iOS应用的5种状态
not running: 没有运行或者被系统终止   
Inactive:      正在进入前台，不能接收事件
Active:        能接收事件
Background: 后台，依然可执行代码，如果可执行代码结束，进入挂起
Suspended:  不能执行代码，如果内存不够，会被终止

//状态的保存恢复
application:shouldSavaeApplicationState	应用退出时调用，控制是否允许保存状态
application:shouldRestoreApplicationState	应用启动时调用，是否恢复上次退出时的状态
application:willEncodeResorableStateWithCoder	保存状态时调用，实现UI状态的保存
application:didDecodeRestorableStateWithCoder	恢复时调用，恢复上次保存的数据
实现具体界面控件的保持和恢复，要在相应viewcontroller中添加代码
-(void)encodeRestorableStateWithCoder:(NSCoder *)coder{
    [super encodeRestorableStateWithCoder:coder];
    [coder encodeObject:self.txtField.text forKey:kSaveKey];
}

-(void)decodeRestorableStateWithCoder:(NSCoder *)coder{
    [super decodeRestorableStateWithCoder:coder];
    self.txtField.text = [coder decodeObjectForKey:kSaveKey];
}

反射
Class viewControllerKlass = NSClassFromString(@"xxxxViewController");
NSAssert(viewControllerKlass, @"Class should not be nil!");
NSAssert([viewControllerKlass isSubclassOfClass:[UIViewController class]], @"Class should be a view controller!");
UIViewController *demoViewController = [[viewControllerKlass alloc] initWithNibName:nil bundle:nil];
