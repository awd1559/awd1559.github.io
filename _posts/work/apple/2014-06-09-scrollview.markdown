---
layout:     post
title:      "scrollview"
subtitle:   " \"scrollview\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - iOS
---
ScrollView

contentSize scrollview中内容的大小content size，所有内容的大小
contentOffset  scrollview滚动的位置
contaentInset  四周增加额外的滚动区域


-(void) viewWillAppear:(BOOL)animated {
    //注册键盘出现通知
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector (keyboardDidShow:) name: UIKeyboardDidShowNotification object:nil];
    //注册键盘隐藏通知
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector (keyboardDidHide:) name: UIKeyboardDidHideNotification object:nil];
   [super viewWillAppear:animated];
}
-(void) viewWillDisappear:(BOOL)animated {
    //解除键盘出现通知
    [[NSNotificationCenter defaultCenter] removeObserver:self  name: UIKeyboardDidShowNotification object:nil];
    //解除键盘隐藏通知
    [[NSNotificationCenter defaultCenter] removeObserver:self name: UIKeyboardDidHideNotification object:nil];
    [super viewWillDisappear:animated];
}






回车取消键盘显示
#pragma mark — UITextFieldDelegate 
- (BOOL)textFieldShouldReturn:(UITextField *)textField
{
    [textField resignFirstResponder];
    return YES;
}






CGRect screenRect = self.window.bounds;
UIScrollView *scrollView = [[UIScrollView alloc] initWithFrame:screenRect];
scrollView.pagingEnabled = YES;
[self.window addSubview:scrollView];


