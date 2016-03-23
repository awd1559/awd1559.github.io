---
layout:     post
title:      "AGEmojiKeyboard"
subtitle:   " \"AGEmojiKeyboard\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
AGEmojiKeyboard
https://github.com/ayushgoel/AGEmojiKeyboard
pod "AGEmojiKeyboard"


#import "AGEmojiKeyboard.h"
AGEmojiKeyboardView *emojiKeyboardView = [[AGEmojiKeyboardView alloc] initWithFrame:CGRectMake(0, 0, self.view.frame.size.width, 216) dataSource:self];
emojiKeyboardView.autoresizingMask = UIViewAutoresizingFlexibleHeight;
emojiKeyboardView.delegate = self;
self.textView.inputView = emojiKeyboardView;


- (void)emojiKeyBoardView:(AGEmojiKeyboardView *)emojiKeyBoardView didUseEmoji:(NSString *)emoji {
  self.textView.text = [self.textView.text stringByAppendingString:emoji];
}

- (void)emojiKeyBoardViewDidPressBackSpace:(AGEmojiKeyboardView *)emojiKeyBoardView {

}
- (UIImage *)emojiKeyboardView:(AGEmojiKeyboardView *)emojiKeyboardView imageForSelectedCategory:(AGEmojiKeyboardViewCategoryImage)category {
  UIImage *img = [self randomImage];
  [img imageWithRenderingMode:UIImageRenderingModeAlwaysOriginal];
  return img;
}

- (UIImage *)emojiKeyboardView:(AGEmojiKeyboardView *)emojiKeyboardView imageForNonSelectedCategory:(AGEmojiKeyboardViewCategoryImage)category {
  UIImage *img = [self randomImage];
  [img imageWithRenderingMode:UIImageRenderingModeAlwaysOriginal];
  return img;
}

- (UIImage *)backSpaceButtonImageForEmojiKeyboardView:(AGEmojiKeyboardView *)emojiKeyboardView {
  UIImage *img = [self randomImage];
  [img imageWithRenderingMode:UIImageRenderingModeAlwaysOriginal];
  return img;
}