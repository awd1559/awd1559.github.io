---
layout:     post
title:      "ios framework"
subtitle:   " \"ios framework\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - apple
---
ModalViewController *modalViewController = [self.storyboard instantiateViewControllerWithIdentifier:@"modalViewController"];
modalViewController.modalTransitionStyle = UIModalTransitionStyleCoverVertical;
[self presentViewController:modalViewController animated:YES completion:nil];

从下部弹出的窗口
[[NSNotificationCenter defaultCenter] addObserver:self
                                             selector:@selector(registerCompletion:)
                                                 name:@"RegisterCompletionNotification"
                                               object:nil];

UIStoryboard* mainStoryboard = [UIStoryboard storyboardWithName:@"MainStoryboard" bundle:nil];
    UIViewController *registerViewController = [mainStoryboard instantiateViewControllerWithIdentifier:@“registerViewController"];        //storyboard id 
    
    registerViewController.modalTransitionStyle = UIModalTransitionStyleCoverVertical;
    [self presentViewController:registerViewController animated:YES completion:^{
        NSLog(@"Present Modal View");
    }];

-(void)registerCompletion:(NSNotification*)notification {
    
    NSDictionary *theData = [notification userInfo];
    NSString *username = [theData objectForKey:@"username"];
    
    NSLog(@"username = %@",username);
}

弹出窗口返回
[self dismissViewControllerAnimated:YES completion:^{
        NSLog(@"Modal View done");
        
        NSDictionary *dataDict = [NSDictionary dictionaryWithObject:self.txtUsername.text  forKey:@"username"];
        [[NSNotificationCenter defaultCenter]
                postNotificationName:@"RegisterCompletionNotification"
                object:nil
                userInfo:dataDict];
        
    }];

ModalViewController *modalViewController = [self.storyboard instantiateViewControllerWithIdentifier:@“modalViewController"];
modalViewController.modalTransitionStyle = UIModalTransitionStyleCoverVertical;
[self presentViewController:modalViewController animated:YES completion:nil];