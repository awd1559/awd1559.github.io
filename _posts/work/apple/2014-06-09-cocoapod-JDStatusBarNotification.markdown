JDStatusBarNotification
https://github.com/jaydee3/JDStatusBarNotification

/install
pod ‘JDStatusBarNotification'

//use 
+ (JDStatusBarView*)showWithStatus:(NSString *)status;
+ (JDStatusBarView*)showWithStatus:(NSString *)status
                      dismissAfter:(NSTimeInterval)timeInterval;

+ (JDStatusBarView*)showWithStatus:(NSString *)status
                         styleName:(NSString*)styleName;

+ (JDStatusBarView*)showWithStatus:(NSString *)status
                      dismissAfter:(NSTimeInterval)timeInterval
                         styleName:(NSString*)styleName;

//关闭
+ (void)dismiss;
(void)dismissAfter:(NSTimeInterval)delay;
//显示进度
(void)showProgress:(CGFloat)progress;  // Range: 0.0 - 1.0

//active
+ (void)showActivityIndicator:(BOOL)show
               indicatorStyle:(UIActivityIndicatorViewStyle)style;


Animation Types
	•	JDStatusBarAnimationTypeNone
	•	JDStatusBarAnimationTypeMove
	•	JDStatusBarAnimationTypeBounce
	•	JDStatusBarAnimationTypeFade
Progress Bar Positions
	•	JDStatusBarProgressBarPositionBottom
	•	JDStatusBarProgressBarPositionCenter
	•	JDStatusBarProgressBarPositionTop
	•	JDStatusBarProgressBarPositionBelow
	•	JDStatusBarProgressBarPositionNavBar


//swift
bridge.h


