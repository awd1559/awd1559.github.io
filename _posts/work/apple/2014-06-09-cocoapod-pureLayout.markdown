https://github.com/PureLayout/PureLayout
 支持swift和OC

pod init
in Podfile
	pod ‘PureLayout'
pod install


#import “PureLayout.h"
全部文档在头文件里

-(void)updateViewConstraints
{
//中心
//in center of superView
self.view autoCenterInSuperview

//长、宽
//width:50, height: 50
self.view autoSetDimensionsToSize:CGSizeMake(50.0, 50.0)
//view.height = 25
self.view autoSetDimension:ALDimensionHeight toSize:25.0


//view.width = blueView.width
self.view autoMatchDimension:ALDimensionWidth toDimension:ALDimensionWidth ofView:self.blueView

//对齐
//view.top = blueView.bottom
self.view autoPinEdge:ALEdgeTop toEdge:ALEdgeBottom ofView:self.blueView
self.view  autoPinEdge:ALEdgeTop toEdge:ALEdgeBottom ofView:self.redView withOffset:10.0


self.view  autoPinEdgeToSuperviewEdge:ALEdgeLeft withInset:20.0


}

[view autoCenterInSuperview];					//view垂直水平居中
[view autoSetDimensionsToSize:CGSizeMake(50.0, 50.0)];		//view大小
[view autoSetDimension:ALDimensionHeight toSize:40.0];		//高度

//red的top与blue的底对齐
[self.redView autoPinEdge:ALEdgeTop toEdge:ALEdgeBottom ofView:self.blueView withOffset:10.0];

//red的宽度与blue的宽度相同
[self.redView autoMatchDimension:ALDimensionWidth toDimension:ALDimensionWidth ofView:self.blueView];



