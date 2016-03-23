---
layout:     post
title:      "SnapKit"
subtitle:   " \"SnapKit\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
https://github.com/SnapKit/SnapKit


//install
use_frameworks!

pod 'SnapKit', '~> 0.15.0'



import SnapKit

class MyViewController: UIViewController {

    lazy var box = UIView()

    override func viewDidLoad() {
        super.viewDidLoad()

        self.view.addSubview(box)
        box.snp_makeConstraints { (make) -> Void in
           make.width.height.equalTo(50)
           make.center.equalTo(self.view)
        }
    }

}

make.size.equalTo(CGSize(width: 500, height: 500))
make.edges.equalTo(UIEdgeInsets(top:10, left: 10, bottom:10, right:10))

make.left.equalTo(view).offset(20)
	   	.lessThanOrEqualTo
		.greaterThanOrEqualTo

make.left.equalTo(view.snp_right)


view.snp_left
view.snp_right
view.snp_top
view.snp_bottom
view.snp_leading
view.snp_trailing
view.snp_width
view.snp_height
view.snp_centerX
view.snp_centerY
view.snp_baseline

