---
layout:     post
title:      "重写UICollectionReusableView"
subtitle:   " \"重写UICollectionReusableView\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - iOS
---

```
UICollectionViewFlowLayout *flowLayout = [UICollectionViewFlowLayout alloc] init;

self.myCollectionView = [UICollectionView alloc] initWithFrame:CGRectMake() collectionViewLayout:flowLayout
self.myCollectionView.backgroundColor = [UIColor];
self.myCollectionView registerClass: [UICollectionViewCell class] forCellWithReuseIdentifier:@""
self.myCollectionView.delegate = self;
self.myCollectionView.dataSource = self;

self.view addSubview:self.myCollectionView;
```

Layout决定CollectinView如何显示在界面上
FlowLayout是一个Cells的线性布局方案， 具有header & footer
定制：
sizeForItemAtIndexPath
minimumInteritemSpacingForSectionAtIndex
referenceSizeForHeaderInSection
referenceSizeForFooterInSection
insetForSectionAtIndex


UICollectionViewDataSource
numberOfSectionsInCollectionView
numberOfItemsInSection
cellForItemAtIndexPath
viewForSupplementaryElementOfKind atIndexPath



UICollectionViewDelegate
