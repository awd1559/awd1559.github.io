---
layout:     post
title:      "Alamofire"
subtitle:   " \"Alamofire\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
//读取文件
NSBundle *bundle = [NSBundle mainBundle];
NSString *plistPath = [bundle pathForResource:@“events" ofType:@"plist"];
//获取属性列表文件中的全部数据
NSArray *array = [[NSArray alloc] initWithContentsOfFile:plistPath];
self.events = array;  

#pragma mark - UICollectionViewDataSource
- (NSInteger)numberOfSectionsInCollectionView:(UICollectionView *)collectionView

- (NSInteger)collectionView:(UICollectionView *)collectionView numberOfItemsInSection:(NSInteger)section


- (UICollectionViewCell *)collectionView:(UICollectionView *)collectionView cellForItemAtIndexPath:(NSIndexPath *)indexPath
{
    Cell *cell = [collectionView dequeueReusableCellWithReuseIdentifier:@"Cell" forIndexPath:indexPath];
    NSDictionary *event = [self.events objectAtIndex:(indexPath.section*2 + indexPath.row)];
    cell.label.text = [event objectForKey:@"name"];
    cell.imageView.image = [UIImage imageNamed:[event objectForKey:@"image"]];
    return cell;
}

#pragma mark - UICollectionViewDelegate
- (void)collectionView:(UICollectionView *)collectionView didSelectItemAtIndexPath:(NSIndexPath *)indexPath
{
    NSDictionary *event = [self.events objectAtIndex:(indexPath.section*2 + indexPath.row)];
    NSLog(@"select event name : %@", [event objectForKey:@"name"]);

}

