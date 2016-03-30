---
layout:     post
title:      "RxSwift"
subtitle:   " \"RxSwift\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
RxSwift
https://github.com/ReactiveX/RxSwift


pod ‘RxSwift’
pod ‘RxCocoa’
pod ‘RxBlocking’

import RxSwift




Observable 背观察的对象，是一个事件序列，
信号分：
热信号：创建时就开始推送，在创建之后订阅的将收不到热信号
冷信号：只有被订阅后，才会推送


Observable
textField.rx_text 获得 Observable<String>



信号操作
map
bindTo
addDisposableTo
shareReplay



创建自己的Observable
func myJust<E>(element: E) -> Observable<E> {
    return Observable.create { observer in
        observer.on(.Next(element))
        observer.on(.Completed)
        return NopDisposable.instance
    }
}

myJust(0)
    .subscribeNext { n in
      print(n)
    }
