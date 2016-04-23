---
layout:     post
title:      "RxAndroid,RxJava"
subtitle:   " \"RxAndroid based on RxJava\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
><small>[RxJava](https://github.com/ReactiveX/RxJava)</small>
><small>[RxAndroid](https://github.com/ReactiveX/RxAndroid)</small>
><small>目录:[gradle](/2014/06/09/gradle)</small>


><small>[RxSwift](https://github.com/ReactiveX/RxSwift)</small>
><small>[RxKotlin](https://github.com/ReactiveX/RxKotlin)</small>

><small>[ReactiveCocoa](https://github.com/ReactiveCocoa/ReactiveCocoa)</small>

Artical 
- [给 Android 开发者的 RxJava 详解](http://gank.io/post/560e15be2dca930e00da1083)


# install

```
compile 'io.reactivex:rxandroid:1.1.0'
compile 'io.reactivex:rxjava:1.1.0'
```

# usage

#### Observer, Subscriber

```
Observer<String> observer = new Observer<String>() {
  @Override
  public void onNext(String s) {}

  @Override
  public void onCompleted() {}

  @Override
  public void onError(Throwable e) {}
};

Subscriber<String> subscriber = new Subscriber<String>() {
  @Override
  public void onNext(String s) {}

  @Override
  public void onCompleted() {}

  @Override
  public void onError(Throwable e) {}
};
```

#### Observable

```
Observable observable = Observable.create(new Observable.OnSubscribe<String>() {
  @Override
  public void call(Subscriber<? super String> subscriber) {
    subscriber.onNext("Hello");
    subscriber.onNext("Hi");
    subscriber.onNext("Aloha");
    subscriber.onCompleted();
  }
});


// from(), just()

Observable<String> o = Observable.from("a", "b", "c");
// onNext("Hello");
// onNext("Hi");
// onNext("Aloha");
// onCompleted();


int[] list = [5, 6, 7, 8]
Observable<Int> o = Observable.from(list);

Observable<String> o = Observable.just("one object");
```

#### Subscribe

```
observable.subscribe(observer);
// or: 
observable.subscribe(subscriber);

// the reasone that not write as observer.subscribe(observable) is because 
// need to chain the functon calls
```

#### example

```
String[] folders;

Observable.from(folders)
    .flatMap(new Func1<File, Observable<File>>() {
        @Override
        public Observable<File> call(File file) {
            return Observable.from(file.listFiles());
        }
    })
    .filter(new Func1<File, Boolean>() {
        @Override
        public Boolean call(File file) {
            return file.getName().endsWith(".png");
        }
    })
    .map(new Func1<File, Bitmap>() {
        @Override
        public Bitmap call(File file) {
            return getBitmapFromFile(file);
        }
    })
    .subscribeOn(Schedulers.io())
    .observeOn(AndroidSchedulers.mainThread())
    .subscribe(new Action1<Bitmap>() {
        @Override
        public void call(Bitmap bitmap) {
            imageCollectorView.addImage(bitmap);
        }
    });

// Lambda
Observable.from(folders)
    .flatMap((Func1) (folder) -> { Observable.from(file.listFiles()) })
    .filter((Func1) (file) -> { file.getName().endsWith(".png") })
    .map((Func1) (file) -> { getBitmapFromFile(file) })
    .subscribeOn(Schedulers.io())
    .observeOn(AndroidSchedulers.mainThread())
    .subscribe((Action1) (bitmap) -> { imageCollectorView.addImage(bitmap) });
```

#### Scheduler

| ---------------------------- | -------------------------------------- |
|Schedulers.immediate()        |by default, on the same thread          |
|Schedulers.newThread()        |always on new thread                    |
|Schedulers.io()               |io op, same as newThread, in Thread pool|
|Schedulers.computation()      |thread pool contains cpu's count thread |
|AndroidSchedulers.mainThread()|for android ui thread                   |

```
Observable.just(1, 2, 3, 4)
    .subscribeOn(Schedulers.io()) //produce event on io thread pool
    .observeOn(AndroidSchedulers.mainThread()) //consume event on android ui thread
```

