---
layout:     post
title:      "storyboard"
subtitle:   " \"storyboard\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
category: apple
permalink: /apple/storyboard
tags:
    - Apple
---
><small>目录:[Apple目录](/apple/)</small>




# StoryBoard

#### navigation
> - 拖入一个Navigation Controller到storyboard, 属性设为Is Initial View Controller
> - 拖入普通的ViewController
> - ctrl+鼠标左键: 从Navigation Contrller上拖动到ViewController， 选择 root view controller
> - or
> - Editor -> Embedded in -> Navigation Controller
> - 可以修改Navigation Item




#### 跳转时带参数
> - Segue就是类UIStoryboardSegue的实例
> - 当跳转时当前视图会收到prepareForSegue:send:消息

```
-(void)prepareForSegue:(UIStoryboardSegue *) segue sender:(id)sender{
    secondViewController* second = segue.destinationViewController;        
    [second setText: myInput.text];                  //实例未初始化nib
}
```



#### tab
> - storyboard中添加Tab Bar Controller
> - or
> - Editor -> Embeded in -> Tab bar Controller




#### 多StoryBoard

> - 新建sub.storyboard文件， 定义ViewController
> - 设为Is Initial View Controller
> - 在Main.storyboard中添加Storyboard Reference, 指向sub.storyboard


 
#### [IBAnimatable](https://github.com/JakeLin/IBAnimatable)
> - animation design in Storyboard
> - drag UIView into storyboard，set corresponded AnimatableView
> - prototype tool, as good as Axure RP

|UIKit elements         |Animatable UI elements         |
| --------------------- | ----------------------------- |
|UIView                 |AnimatableView                 |
|UIBarButtonItem        |AnimatableBarButtonItem        |
|UIButton               |AnimatableButton               |
|UIButton               |AnimatableCheckBox             |
|UIImageView            |AnimatableImageView            | 
|UILabel                |AnimatableLabel                |
|UIStackView            |AnimatableStackView            |
|UITableView            |AnimatableTableView            |
|UITableViewCell        |AnimatableTableViewCell        | 
|UITextField            |AnimatableTextField            | 
|UITextView             |AnimatableTextView             |
|UINavigationBar        |DesignableNavigationBar        |
|UIViewController       |AnimatableViewController       |
|UINavigationController |AnimatableNavigationController |

