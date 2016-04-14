---
layout:     post
title:      "Event Bus"
subtitle:   " \"Android Eventbus by greenbot\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
><small>[EventBus](https://github.com/greenrobot/EventBus)</small>
><small>目录:[gradle](/2014/06/09/gradle)</small>

simplifies communication between Activities, Fragments, Threads, Services

# install

```
compile 'org.greenrobot:eventbus:3.0.0'
```

# usage

#### 1.define event

```
public class MessageEvent {
    public final String message;

    public MessageEvent(String message) {
        this.message = message;
    }
}
```


#### 2.Prepare subscribers

```
@Override
public void onStart() {
    super.onStart();
    EventBus.getDefault().register(this);
}

@Override
public void onStop() {
   EventBus.getDefault().unregister(this);
   super.onStop();
}

@Subscribe
public void onEvent(MessageEvent event) {
  /* Do something */
}
```

#### 3.post event

```
EventBus.getDefault().post(new MessageEvent("send message"));
```
