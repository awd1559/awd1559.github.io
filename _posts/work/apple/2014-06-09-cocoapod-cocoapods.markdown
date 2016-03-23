安装
sudo gem install -g cocoapods
sudo gem uninsall cocoapods

pod setup    #设置环境

pod init          #创建一个Podfile文件
pod install
pod update


//制作cocoapods
pod trunk register awd1559@gmail.com 'awd1559' //注册

//生成SwiftyExt.podspec
pod spec create NAME
//检查
pod spec lint SwiftyExt.podspec  
//添加到本地repo spec
pod repo push SPECNAME NAME.podspec

git tag '1.0.0'
git push —tags
//删除原称tag
git push origin —delete tag <tagnaem>  

//上传到cocoapods
pod trunk push SwiftyExt.podspec  





常用的pod
autolayout
	masonry
	neon
	purelayout
	SnapKit 
用起来都不是很好，直接食用Storyboard，可以很好很直观的解决问题
storyboard中还可以使用tab、nav、跳转

ReactiveCocoa/RxSwift
KVOController

网络
SDWebImage
AFNetworking
Alamofire

动画
pop

布局
MJRefresh
XLPagerTabStrip
RDVTabBarController
RKSwipeBetweenViewControllers
RESideMenu/DrawerController
HUD
	MBProgressHUD
	SVProgressHUD
	JGProgressHUD

引导页
JazzHands

JSON
Objectmapper
Ono
SwiftJSON

加强
DateTool
Timepiece
FontAwesome
FontAwesome.swift

Log
XCGLogger
