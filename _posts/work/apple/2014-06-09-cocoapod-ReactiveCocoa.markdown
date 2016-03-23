---
layout:     post
title:      "ReactiveCocoa"
subtitle:   " \"ReactiveCocoa\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
事件处理方式
action
delegate
KVO
callback
NSNotification 
ReactiveCocoa为事件定义一个标准接口

/////////////////
// install
/////////////////
use_frameworks!
pod 'ReactiveCocoa'

Cartfile
github "ReactiveCocoa/ReactiveCocoa"
carthage update


创建信号
self.usernameTextField  .rac_textSignal    subscribeNext:^(id value){}
self.usernameTextField  .rac_textSignal   filter:^(id value){}    subscribeNext: ^(id value){}
filter:过滤signal

RACSignal *signal = self.usernameTextField.rac_textSignal;

map函数
从上一个next事件接收数据，通过执行block把返回值传给下一个next事件。
self.usernameTextField.rac_textSignal
    map:^id(NSString* text){ return @(text.length);}
    filter:^BOOL(NSNumber* length ){}
    subscribeNext:^(id x){};

转换信号，修改背景色，实际不使用如下写法
RACSignal *validPasswordSignal = [self.passwordTextField.rac_textSignal 
		 map:^id(NSString *text) { 
		 return @([self isValidPassword:text]);
}];

[[validPasswordSignal
   map:^id(NSNumber *passwordValid){return[passwordValid boolValue] ? [UIColor clearColor]:[UIColor yellowColor];
}]
	 subscribeNext:^(UIColor *color){
	    self.passwordTextField.backgroundColor = color;
}];

使用如下写法
RAC(self.passwordTextField, backgroundColor) = [validPasswordSignal
	map:^id(NSNumber *passwordValid){
		return[passwordValid boolValue] ? [UIColor clearColor]:[UIColor yellowColor];
}];






聚合信号
RACSignal *signUpActiveSignal =
  [RACSignal combineLatest:@[validUsernameSignal, validPasswordSignal]
      reduce:^id(NSNumber*usernameValid, NSNumber *passwordValid){
          return @([usernameValid boolValue]&&[passwordValid boolValue]);
}];



系统事件信号
[[[self.cancelButton 
	rac_signalForControlEvents:UIControlEventTouchUpInside] 
	takeUntil:self.rac_prepareForReuseSignal] 
	subscribeNext:^(UIButton *x) { 
}]; 




//siwft
bridge.h
#import <ReactiveCocoa/ReactiveCocoa.h>
import ReactiveCocoa

button.rac_signalForControlEvents(UIControlEvents.TouchUpInside)
            .subscribeNext{  _ in
                print("this button touchupinside")
}


let signal = RACSignal.ceateSignal({ (subscriber: RACSubscriber!) -> RACDisposable! in
	let data = NSData(contentsOfURL: imageUrl)
	let image = UIImage(data: data!)
	subscriber.sendNext(image)
	subscriber.sendCompleted()
	return nil
})
let scheduler = RACScheduler(priority: RACSchedulerPriorityBackground)
return signal.subscribeOn(scheduler)



使用ReactiveSwiftFlickrSearch中的RACObserve.swift, RAC.swift, RACSignal+Extensions.swift
atext.rac_textSignal() ~> RAC(label, “text”)

btext.rac_textSignal().map({text in
	if (text as! String).characters.count > 0 {
		return true
	} else {
		return false
	}
}) ~> RAC(button, “enabled")

RACSignalEx.combineLatestAs([favouritesSignal, commentsSignal]) {
      (favourites:String, comments:String) -> Bool in
     return false
    }