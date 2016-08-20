---
layout: post
title: "first blog"
date: 2016-06-07 11:03:02 +0800
comments: true
categories: 
---

# DDNote

## **Algorithm**
* [Direct insertion sort](http://www.henishuo.com/insert-sort/)
* [张不坏的博客](http://zhangbuhuai.com/2015/06/28/Array-and-Algorithm/)



## Animaton
### TransitionAnimation
* [VCTransitionsLibrary](https://github.com/ColinEberhardt/VCTransitionsLibrary)
* [RZTransitions](https://github.com/Raizlabs/RZTransitions)
* [HYBControllerTransitions](https://github.com/CoderJackyHuang/HYBControllerTransitions)
* [KYMagicMove](https://github.com/KittenYang/KYMagicMove)
* [ViewControllersTransition](https://github.com/YouXianMing/ViewControllersTransition)
* [iOS-ViewController-Transition-Demo](https://github.com/seedante/iOS-ViewController-Transition-Demo.git)
* [ZFDragableModalTransition(淘宝进入购买详情转场动画)](https://github.com/zoonooz/ZFDragableModalTransition)

### CollectionAnimation
* [popping](https://github.com/schneiderandre/popping)

### facebookPopMenuAnimation
* [DXPopover](https://github.com/xiekw2010/DXPopover)
* [CMPopTipView](https://github.com/chrismiles/CMPopTipView)
* [NirKxMenu](https://github.com/zpz1237/NirKxMenu)

### TinderSwipeAnimation
* [MDCSwipeToChoose](https://github.com/modocache/MDCSwipeToChoose)
* [TinderSimpleSwipeCards](https://github.com/cwRichardKim/TinderSimpleSwipeCards)
* [ZLSwipeableView](https://github.com/zhxnlai/ZLSwipeableView)
* [Koloda](https://github.com/Yalantis/Koloda)
* [HotGirls](https://github.com/zangqilong198812/HotGirls)

### GestureAnimation
* [DraggableYoutubeFloatingVideo](https://github.com/vizllx/DraggableYoutubeFloatingVideo)


## Video
### AVFoundation
* [iOS使用AVFoundation实现二维码扫描](http://strivingboy.github.io/blog/2014/11/08/scan-qrcode/)  
* [AVFoundation Tutorial](https://www.raywenderlich.com/30200/avfoundation-tutorial-adding-overlays-and-animations-to-videos)
* [AVFoundation Take photo](http://www.jianshu.com/p/6dd23699f92f)
* [liveVideoIntroductionBiaoGeBlog](http://www.henishuo.com/ios-live-confused/)
* [book](http://item.jd.com/11742630.html)

* [Bilibili / ijkplayer baseed on FFmpeg with MediaCodec,Video Toolbox support](https://github.com/Bilibili/ijkplayer)

* [AVFoundation 视频流处理](https://github.com/100mango/zen/blob/master/iOS学习：AVFoundation%20视频流处理/iOS学习：AVFoundation%20视频流处理%20.md)

* [SCRecorder iOS camera engine with Vine-like tap to record, animatable filters, slow motion, segments editing](https://github.com/rFlex/SCRecorder.git)

* [ffmpeg principle](https://segmentfault.com/a/1190000000502967)

* [Cache media file while play media using AVPlayer](https://github.com/vitoziv/VIMediaCache)

* [AVFoundation编程指南1-使用 Assets](https://segmentfault.com/a/1190000004049416)

* [AVFoundation编程指南2-用AVPlayer播放视频](https://segmentfault.com/a/1190000004054258)
* [AVFoundation相关类的分析](http://www.fanliugen.com/?p=423)
* [iOS 视频剪切、旋转，视频添加音频、添加水印，视频导出](http://ios.jobbole.com/85309/)
* [iOS 三种录制视频方式](http://ios.jobbole.com/85069/)
* [CMTime简单介绍](http://www.jianshu.com/p/f110bf6e0471)
* [AVFoundation(一):基础知识](http://www.jianshu.com/p/485e946f80b4)
* [AVFoundation(二)：核心AVAsset](http://www.jianshu.com/p/9805be76ee68)
* [iOS音视频实现边下载边播放](http://sky-weihao.github.io/2015/10/06/Video-streaming-and-caching-in-iOS/)
* [CTVideoPlayerView](https://github.com/casatwy/CTVideoPlayerView)
* [Eleven Player is a simple powerful video player.use ffmpeg](https://github.com/coderyi/Eleven)

```
CMTimeMake和CMTimeMakeWithSeconds 详解 
CMTimeMake(a,b)    a当前第几帧, b每秒钟多少帧.当前播放时间a/b
CMTimeMakeWithSeconds(a,b)    a当前时间,b每秒钟多少帧.
CMTimeMake
CMTime CMTimeMake (
   int64_t value,
   int32_t timescale
);
CMTimeMake顧名思義就是用來建立CMTime用的,
但是千萬別誤會他是拿來用在一般時間用的,
CMTime可是專門用來表示影片時間用的類別,
他的用法為: CMTimeMake(time, timeScale)
time指的就是時間(不是秒),
而時間要換算成秒就要看第二個參數timeScale了.
timeScale指的是1秒需要由幾個frame構成(可以視為fps),
因此真正要表達的時間就會是 time / timeScale 才會是秒.
簡單的舉個例子
CMTimeMake(60, 30);
CMTimeMake(30, 15);
```



### muke
 * [segmentfault iOS share](http://www.imooc.com/learn/599)
 * [beijing swift conference](http://www.imooc.com/learn/600)

### Download
* [MJDownload](https://github.com/CoderMJLee/MJDownload.git)
* [ZFPlayer](https://github.com/renzifeng/ZFPlayer.git)
* [TCBlobDownload](https://github.com/thibaultCha/TCBlobDownload.git)

```
Features
     后台下载文件
	1	Download files in background threads
	   代理或者blocks风格
	2	Blocks or delegate style
	   暂停 重新开始一个下载
	3	Pause and resume a download
	   设置最大并发下载数
	4	Set a maximum number of concurrent downloads
	   自定义下载路径
	5	Custom download path
	   下载速度与剩余时间
	6	Download speed and remaining time
	   取消下载
	7	Download cancellation
	    下载依赖 
	8	Download dependencies
	
	•	If a download has been stopped and the local file has not been deleted, when you will restart the download to the same local path, the download will start where it has stopped using the HTTP Range header (14.35).
	•	You can also set dependencies in your downloads using the addDependentDownload: method from TCBlobDownloader.
```

[MZDownloadManager(swfit now)](https://github.com/mzeeshanid/MZDownloadManager)

```
This download manager uses the iOS 7 NSURLSession api to download files.
     能在后台下载大的文件
	•	Can download large files if app is in background.
	   能在后台下载文件
	•	Can download files if app is in background.
	   能在同一时间下载多个文件
	•	Can download multiple files at a time.
	   重新开始下载已经打断的下载任务
	•	It can resume interrupted downloads.
	   用户能够暂停下载
	•	User can also pause the download.
	   如果任何错误发生了，用户能够重新下载
	•	User can retry any download if any error occurred during download.
```


* [Download-Manager](https://github.com/oarrabi/Download-Manager)

```
What it provides
	•	Easy to integrate and use iOS download manager.
	•	Easily download file with the very robust AFNetworking library.
	•	Deal only with NSURL, you will never have to keep strong or weak references of the Download managers.
	•	Download files in sequential and parallel order.
	•	Make sure each file (NSURL) is being downloaded only once.
	•	Have multiple listener/delegates on a single download operation.
	•	Download operation unique by URL, never download a URL twice.
	•	Cache the downloaded file in Memory and on Disk using EGOCache.
	•	Easily add and remove listeners to observe the download operations.
	•	Singleton classes for fast access and minimum memory overhead.
	•	Ensure that the UI Thread is never blocked.
	•	Delegate or Block event callbacks.
	•	All of the above in two lines of code.

```
 **downloadManager should do**
 
```
 1. 后台下载
 2. 多任务下载
 3. 暂停
 4. 多任务暂停
 5. 全部暂停
 6. delete
 7. 多任务delete
 8. 全部delete
 9. 返回下载状态（1：没有下载 2：下载中 3：下载成功 4：下载失败：5：其他）
 10. 检测某个任务是否正在下载
 11. 查看已经下载文件存放位置（readonly）
 12. 查看已经下载文件大小（readonly）
 13. 查看已经下载文件名（readonly）
 14. 查看已经下载文件类型（readonly）
 15. 查看已经下载成功的时间（readonly）
 13. 下载中文件的进度
 14. 设置下载任务的优先级
 15. 设置断点续传
 16. 检测已经下载的文件是否完整
 17. 查看文件开始下载的时间(readonly)
 18. 检测已经下载的文件
 19. 检测全部已经下载文件的大小
 20. 设置下载超时时间
 21. 设置cdnurl
 22. 查看正在下载的文件数量
 23. 删除过期的文件
 24. 设置删除过期的文件的算法
 25. 查询正在下载的任务
 26. 查询某个下载任务的进度
 27. 
```



### LiveVideo
* [LiveVideoCoreSDK](https://github.com/runner365/LiveVideoCoreSDK)
* [SmarterStreaming](https://github.com/daniulive/SmarterStreaming)
* [主流跨平台媒体库ffmpeg，live555，MobileVLCKit简介](https://segmentfault.com/a/1190000002953107)
* [MiaowShow iOS视频直播项目](https://github.com/SunLiner/MiaowShow)

##Audio
* [MPVolumeView_iOS program modification system volume](https://segmentfault.com/a/1190000002401961)

## Image

### Gif 
* [FLAnimatedImage](https://github.com/Flipboard/FLAnimatedImage)
* [sever return 304](http://weibo.com/1247589445/DwgHFs2cF?type=repost)
* [关于UIImage的内存问题与解决方案](https://github.com/Magic-Unique/HXImage/blob/master/description.md)


## View
* [scrollView To Top](http://www.jianshu.com/p/68632cbd6263)
* [why SDWebImageDecoder](http://www.jianshu.com/p/135e17c7d10f)
* [Y_KLine](https://github.com/yate1996/Y_KLine)
* [StockKLine](https://github.com/mengmanzbh/StockKLine)
* [高仿支付宝解锁](https://github.com/CharlinFeng/CoreLock)

### 占位视图
* [DZNEmptyDataSet](https://github.com/dzenbot/DZNEmptyDataSet)
* [CYLTableViewPlaceHolder](https://github.com/ChenYilong/CYLTableViewPlaceHolder)

### MessageKit
* [Atlas-iOS](https://github.com/layerhq/Atlas-iOS)


### Button
* [图片与文字不定Btn](https://github.com/lianchengjiang/LCUIKit)



## CALayer
* [CALayer and subLayer](http://my.oschina.net/u/2340880/blog/536048)
* [CATextLayer](https://github.com/joeshang/CATextLayerTest)

```
普通CALayer在被初始化时是需要给一个frame值的,这个frame值一般都与给定view的bounds值一致,它本
身是有形状的,而且是矩形.
CAShapeLayer在初始化时也需要给一个frame值,但是,它本身没有形状,它的形状来源于你给定的一个path,

然后它去取CGPath值,它与CALayer有着很大的区别
CAShapeLayer有着几点很重要:
1. 它依附于一个给定的path,必须给与path,而且,即使path不完整也会自动首尾相接
2. strokeStart以及strokeEnd代表着在这个path中所占用的百分比
```
* [CAGradientLayer](https://zsisme.gitbooks.io/ios-/content/chapter6/cagradientLayer.html)


## Model
* [YYModel basic knowledge](http://www.jianshu.com/p/198af7042b2d)
* [YYModel 源码历险记](http://www.jianshu.com/users/aa41dad549af/latest_articles)
* [YYModel Part](http://xiongzenghuidegithub.github.io/blog/archives/)

## Cache
* [FMDB](https://github.com/ccgus/fmdb)
* [realm](https://github.com/realm/realm-cocoa)
* [MagicalRecord](https://github.com/magicalpanda/MagicalRecord)
* [VIMediaCache](https://github.com/vitoziv/VIMediaCache)
* [NSURLCache 网络请求缓存指南](http://www.cocoachina.com/ios/20160701/16895.html)

## Text
* [CoreText_xiongzenghu](http://xiongzenghuidegithub.github.io/blog/2016/04/26/coretext-part-3/)
* [CoreText_zoomfeng](http://www.zoomfeng.com/blog/coretextshi-yong-jiao-cheng-%5B%3F%5D.html)
* [TTTAttributedLabel](https://github.com/TTTAttributedLabel/TTTAttributedLabel)
* [UILabel replacement with fine-grain appear/disappear animation](https://github.com/overboming/ZCAnimatedLabel)
* [TYAttrubutedLabel](https://github.com/12207480/TYAttributedLabel)
* [YYText 是如何绘制的](https://github.com/lzwjava/OpenSourceNotes)






## AutoLayout
* [Autolayout standard style of writing](http://reviewcode.cn/article.html?reviewId=14)
* [Masonry 源码解析](https://github.com/Draveness/iOS-Source-Code-Analyze/blob/master/Masonry/iOS%20源代码分析%20---%20Masonry.md)
* [HandyAutoLayout](https://github.com/casatwy/HandyAutoLayout)
* [SDAutoLayout](https://github.com/gsdios/SDAutoLayout)
* [Masonry](https://github.com/SnapKit/Masonry)
* [FDStackView —— Downward Compatible UIStackView](http://blog.wtlucky.com)

## CADisplayLink
* [CADisplayLink](http://www.jianshu.com/p/c35a81c3b9eb)

## Architecture
* [OUT OF OOP-inheritance](http://casatwy.com/tiao-chu-mian-xiang-dui-xiang-si-xiang-yi-ji-cheng.html)
* [IOP](http://casatwy.com/tiao-chu-mian-xiang-dui-xiang-si-xiang-er-duo-tai.html)
* [OUT OF OOP-package](http://casatwy.com/tiao-chu-mian-xiang-dui-xiang-si-xiang-san-feng-zhuang.html)
* [know or understand](http://casatwy.com/zen-yao-mian-shi-jia-gou-shi.html)
* [路由跳转的思考](http://awhisper.github.io/2016/06/12/路由跳转的思考/)
* [CDD](http://mrpeak.cn/blog/cdd/)
* [天猫架构解耦之路 by gaosboy（高嘉峻)](http://weibo.com/1708947107/DBQxn64gC?type=repost#_rnd1467178225666)
* [新浪微博iOS客户端架构与优化之路](http://mp.weixin.qq.com/s?__biz=MzA3ODg4MDk0Ng==&mid=2651112273&idx=1&sn=893a66a04e541a99b7bc4d7cf227e2f7#rd)
* [滴滴出行iOS客户端架构演进之路](http://mp.weixin.qq.com/s?__biz=MzA3ODg4MDk0Ng==&mid=402854111&idx=1&sn=5876e615fabd6d921285d904e16670fb#rd)
* [面向切面编程之 Aspects 源码解析及应用](http://wereadteam.github.io/2016/06/30/Aspects/)
* [解耦神器 —— 统跳协议和Rewrite引擎_Gaosboy](http://pingguohe.net/2015/11/24/Navigator-and-Rewrite.html?from=timeline&isappinstalled=0)


### FRP
* [RAC](https://github.com/ReactiveCocoaChina/ReactiveCocoaChineseResources)

## Memory leaks
* [MLeaksFinder](https://github.com/Zepo/MLeaksFinder)
* [FBRetainCycleDetector](https://github.com/facebook/FBRetainCycleDetector)

## Runloop
* [RunLoopWorkDistribution](https://github.com/diwu/RunLoopWorkDistribution)
* [PerformanceMonitor](https://github.com/suifengqjn/PerformanceMonitor)
* [RunLoop学习笔记](http://www.starming.com/index.php?v=index&view=74)
* [深入理解RunLoop](http://blog.ibireme.com/2015/05/18/runloop/)
* [sunny runloop实战](http://blog.sunnyxx.com/2015/05/17/cell-height-calculation/)
* [NSRunLoop、参与多线程之间的通信](http://xiongzenghuidegithub.github.io/blog/2015/08/21/nsrunloop,-can-yu-duo-xian-cheng-zhi-jian-de-tong-xin/)
* [iOS实时卡顿监控](http://ios.jobbole.com/83742/)

## Runtime
* [翻译-为什么objc_msgSend必须用汇编实现](http://tutuge.me/2016/06/19/translation-why-objcmsgsend-must-be-written-in-assembly/)
* [Objective-C 消息发送与转发机制原理](http://yulingtianxia.com/blog/2016/06/15/Objective-C-Message-Sending-and-Forwarding/)
* [Calling Conventions](http://slides.com/sunnyxx/calling-conventions-in-cocoa#/)
* [如何动态调用 C 函数](http://mp.weixin.qq.com/s?__biz=MzIzNTQ2MDg2Ng==&mid=2247483687&idx=1&sn=94d3ce224e5e25f2e1ae8a6046efb472#rd)

## SQLite
* [GYDataCenter](https://github.com/Zepo/GYDataCenter)
* [CTPersistance](https://github.com/casatwy/CTPersistance)
* [FMDB](https://github.com/ccgus/fmdb)

## Socket
* [微信、陌陌等著名IM软件设计架构详解](http://blog.csdn.net/justinjing0612/article/details/38322353)

##Cocoapods
* [ERROR: While executing gem ... (Errno::EPERM) Operation not permitted - /usr/bin/pod](http://stackoverflow.com/questions/30812777/cannot-install-cocoa-pods-after-uninstalling-results-in-error/30851030#30851030)
* [Operation not permitted - /usr/bin/fuzzy_match](http://blog.csdn.net/sinat_29998157/article/details/50070687)
* [While executing gem ... (TypeError) no implicit conversion of nil into String](http://stackoverflow.com/questions/25844937/how-to-install-cocoa-pods-in-terminal)
* [When using cocoapods, what is the best way to change the PRODUCT_NAME?](http://stackoverflow.com/questions/31120403/when-using-cocoapods-what-is-the-best-way-to-change-the-product-name)
* [理解Cocoapods](https://segmentfault.com/a/1190000005041357)

##SomeGuysBlog
* [WeiXinRead](http://wereadteam.github.io)
* [sunnyxx](http://blog.sunnyxx.com)
* [FMDB_description](http://blog.csdn.net/yixiangboy/article/details/51274186)
* [integration ijkplayer](http://www.jianshu.com/p/1f06b27b3ac0)
* [daiming](http://www.jianshu.com/users/9a4903d7e3d1/latest_articles)
* [Draveness](http://draveness.me/)
* [chuange](http://adad184.com)
* [tutuge](http://tutuge.me)
* [casa](http://casatwy.com)
* [leichunfeng](http://blog.leichunfeng.com)
* [YY](http://blog.ibireme.com)
* [YY github ios list](http://github.ibireme.com/github/list/ios/)
* [onev](https://onevcat.com)
* [youxianming](http://www.cnblogs.com/YouXianMing/)
* [JohnLui](https://lvwenhan.com)
* [mz](http://makezl.github.io)
* [margtin](http://www.martinrgb.com)
* [zhuo](http://www.jianshu.com/users/88a056103c02/latest_articles)
* [tangqiao](http://blog.devtang.com)
* [mrpeak](http://mrpeak.cn)
* [yang](http://kittenyang.com)
* [yanzu](http://www.jianshu.com/users/b82d2721ba07/latest_articles)
* [beige](http://www.henishuo.com)
* [nanfengzi](http://southpeak.github.io)
* [xiongzenghuidegithu](http://xiongzenghuidegithub.github.io)
* [lexrus](http://lexrus.com)
* [xiaobenlang](http://jiangliancheng.gitcafe.io)
* [xia](http://blog.txx.im/?from=inf&wvr=5&loc=infblog)
* [zixun](http://zixun.github.io)
* [zengxianhua](http://zengxianhua.com)
* [kissGod](http://www.jianshu.com/users/8d704c0faf00/latest_articles)
* [bang](http://blog.cnbang.net/archives/)
* [TomatoRead](https://github.com/everettjf/TomatoRead)
* [玉令天下的博客](http://yulingtianxia.com/blog/2016/06/15/Objective-C-Message-Sending-and-Forwarding/)
* [bestswifter](https://bestswifter.com)
* [百度Hi团队 iOS 技术周报](https://github.com/BaiduHiDeviOS/iOS-Tech-Weekly)
* [iOS-Source-Code-Analyze](https://github.com/Draveness/iOS-Source-Code-Analyze)
* [Ghost博客搭建 - 追随猫神之路](http://402v.com/ghostbo-ke-da-jian-xi-lie-zhui-sui-mao-shen-zhi-lu/)
* [MartinRGB](http://www.martinrgb.com)
* [阮一峰的网络日志](http://www.ruanyifeng.com/blog/)
* [iPic](http://toolinbox.net)

## Git
* [Git Flow](http://www.jianshu.com/p/fa83b6858d52)
* [如何解决GitHub commit次数过多.git文件过大的问题?](https://www.zhihu.com/question/29769130)
* [if you change your password or username on GitHub](https://help.github.com/articles/updating-credentials-from-the-osx-keychain/)
* [git 原理](http://gold.xitu.io/entry/575e223a165abd005559294f)

```
git Alias
autoPush() {
    git add -A
    git commit -m $1
    git push
}
alias g=autoPush
```

### Gitpages
* [southpeak.github.io](http://southpeak.github.io)
  
  
## Crash
* [objc_retain] (http://www.bkjia.com/IOSjc/898404.html)
* [NSTimer](http://blog.csdn.net/enuola/article/details/8099461)

```
You must send this message from the thread on which the timer was installed. If
you send this message from another thread, the input source associated with the
timer may not be removed from its run loop, which could prevent the thread from
exiting properly.
NSTimer 在哪个线程创建就要在哪个线程停止，否则会导致资源不能被正确的释放。看起来各种坑还不少。

```

## Efficiency 
* [Mac_MrPeak](http://mrpeak.cn/blog/mac-efficiency/)


## Tool
* [Phabricator](http://phabricator.org/)
* [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)
* [Homebrew](http://brew.sh/)
* [fastlane(`The easiest way to automate building and releasing your iOS and Android apps`)打包Tool](https://github.com/fastlane/fastlane)
* [Charles抓包心得](http://itangqi.me/2016/05/30/tips-for-using-charles/#more)
* [Surge原理](http://gold.xitu.io/entry/562eef4900b0acaac036ac11)
* [WWDC 410 Visual Debugging With Xcode](https://mp.weixin.qq.com/s?__biz=MzIwMTYzMzcwOQ==&mid=2650948410&idx=1&sn=c48375a832b8769a0f43a293a3f09fe3&scene=0&key=f8ab7b995657050bada4064a262d2959647e1b5f90d16dc6aacd29bbb714ed1c9ab7d221648976431d558244cd7f7f4c&ascene=0&uin=NDU1NzA2MTk1&devicetype=iMac+MacBookPro12%2C1+OSX+OSX+10.11.5+build(15F34)&version=11020201&pass_ticket=H4NFpA%2FV2mGlXbz6iuyTOJnJk06Bxbxc4ZX3kEuhqXJbEyQiJG8zuAWpLkapt%2F31)
* [Surge config](https://github.com/lhie1/Surge)
* [AppleDNS](https://github.com/gongjianhui/AppleDNS)
* [alfred workflow 李大锤同学](http://weibo.com/lizexipablo?profile_ftype=1&is_all=1&is_search=1&key_word=alfred#_0)
* [鼠须管](https://github.com/rime/squirrel)
* [Mac  开发者  怕雾霾和没vim  设计师](http://liqi.io/zhangbin/)
* [Mac  Swift  同用书垫电脑  开发者](http://liqi.io/wangling/)



```
homebrew-cask,官网传送, 是一套建立在homebrew基础上的Mac软件安装命令行工具。与brew的区别就
是，后者侧重于软件套件和软件环境的配置安装，而前者是mac平台软件
```

```
brew 是从下载源码解压然后 ./configure && make install ，同时会包含相关依存库。并自动配置好
各种环境变量，而且易于卸载。 
这个对程序员来说简直是福音，简单的指令，就能快速安装和升级本地的各种开发环境。
而 brew cask 是 已经编译好了的应用包 （.dmg/.pkg），仅仅是下载解压，放在统一的目录中（/opt/
homebrew-cask/Caskroom），省掉了自己去下载、解压、拖拽（安装）等蛋疼步骤，同样，卸载相当容易与
干净。这个对一般用户来说会比较方便，包含很多在 AppStore 里没有的常用软件。
```


* [hosts](https://github.com/racaljk/hosts)
* [hacker-scripts](https://github.com/NARKOZ/hacker-scripts)

## Tutorial
* [objc](http://objccn.io)
* [Safari for OS X 你不可不知的 10 个快捷键](http://sspai.com/30902)
* [Markdown](https://github.com/younghz/Markdown)
* [TimLiu-iOS](https://github.com/Tim9Liu9/TimLiu-iOS)
* [链式编程1](http://www.jianshu.com/p/87ef6720a096)
* [链式编程2](http://xiongzenghuidegithub.github.io/blog/2015/12/04/blockmo-ni-lian-shi-yu-fa/)
* [一些 iOS / Web 开发相关的翻译或原创博客文章](https://github.com/nixzhu/dev-blog)
* [YY整理- ( ゜- ゜)つロ Github-iOS备忘](http://github.ibireme.com/github/list/ios/)


## 设计模式
* [youxianming](http://www.cnblogs.com/YouXianMing/tag/软件设计原则/)
* [leichunfeng](https://github.com/leichunfeng/DesignPatterns-Objective-C)



##Foundation
* roundf 将浮点值四舍五入为最接近的整数
* `pow() 函数用来求 x 的 y 次幂（次方），其原型为：
    double pow(double x, double y);`
* `usleep函数能把进程挂起一段时间， 单位是微秒（千分之一毫秒）`


## NetWorking
* [RTNetworking](https://github.com/casatwy/RTNetworking)

1. 以什么方式将数据交付给业务层？这个问题的回答是这样：
   尽可能通过Delegate的回调方式交付数据，这样可以避免不必要的跨层访问。当出现跨层访问的需求时（比如信号类型切换），通过Notification的方式交付数据。正常情况下应该是避免使用Block的。

2. 使用reformer这个对象用于封装数据转化的逻辑，这个对象是一个独立对象，事实上，它是作为Adaptor(适配器)模式

3. 对于业务层而言，由Controller根据View和APIManager之间的关系，选择合适的reformer将View可以直接使用的数据（甚至reformer可以用来直接生成view）转化好之后交付给View。对于网络层而言，只需要保持住原始数据即可，不需要主动转化成数据原型。然后数据采用NSDictionary加Const字符串key来表征，避免了使用对象来表征带来的迁移困难，同时不失去可读性。

* [iOS中的 NSURLProtocol](http://www.jianshu.com/p/0244e431fb3c)

## Optimize
* [可以试试弃用 UILabel，使用 UIView，通过绘制一张圆角+文字的图片作为其 layer 的 contents。](http://reviewcode.cn/article.html?reviewId=7)
* [YYModel 性能优化的几个 Tip：](http://blog.ibireme.com/2015/10/23/ios_model_framework_benchmark/)

## Device
* [getUUID](http://www.henishuo.com/uuid-udid/)

## Xcode 
* [iOS应用程序打包](http://www.jianshu.com/p/bd953c3e389f)

## Http Code description

```
HTTP状态码介绍


HTTP 400    – 请求无效
HTTP 401.1 – 未授权：登录失败
HTTP 401.2 – 未授权：服务器配置问题导致登录失败
HTTP 401.3 – ACL 禁止访问资源
HTTP 401.4 – 未授权：授权被筛选器拒绝
HTTP 401.5 – 未授权：ISAPI 或 CGI 授权失败

HTTP 403      – 禁止访问
HTTP 403      – 对 Internet 服务管理器 的访问仅限于 Localhost
HTTP 403.1 禁止访问：禁止可执行访问
HTTP 403.2   – 禁止访问：禁止读访问
HTTP 403.3   – 禁止访问：禁止写访问
HTTP 403.4   – 禁止访问：要求 SSL
HTTP 403.5   – 禁止访问：要求 SSL 128
HTTP 403.6   – 禁止访问：IP 地址被拒绝
HTTP 403.7   – 禁止访问：要求客户证书
HTTP 403.8   – 禁止访问：禁止站点访问
HTTP 403.9   – 禁止访问：连接的用户过多
HTTP 403.10 – 禁止访问：配置无效
HTTP 403.11 – 禁止访问：密码更改
HTTP 403.12 – 禁止访问：映射器拒绝访问
HTTP 403.13 – 禁止访问：客户证书已被吊销
HTTP 403.15 – 禁止访问：客户访问许可过多
HTTP 403.16 – 禁止访问：客户证书不可信或者无效
HTTP 403.17 – 禁止访问：客户证书已经到期或者尚未生效 HTTP 404.1 -

无法找到 Web 站点
HTTP 404 – 无法找到文件
HTTP 405 – 资源被禁止
HTTP 406 – 无法接受
HTTP 407 – 要求代理身份验证
HTTP 410 – 永远不可用
HTTP 412 – 先决条件失败
HTTP 414 – 请求 – URI 太长

HTTP 500        – 内部服务器错误
HTTP 500.100 – 内部服务器错误 – ASP 错误
HTTP 500-11 服务器关闭
HTTP 500-12 应用程序重新启动
HTTP 500-13  – 服务器太忙
HTTP 500-14  – 应用程序无效
HTTP 500-15  – 不允许请求 global.asa
Error 501       – 未实现
HTTP 502       – 网关错误
```



# 小知识

```
isKindOfClass来确定一个对象是否是一个类的成员，或者是派生自该类的成员
isMemberOfClass只能确定一个对象是否是当前类的成员
```

```
删除Xcode多余描述文件
~/Library/MobileDevice/Provisioning Profiles
```

```
快速入门写接口 Node.js
rnr,flask,express
```

* [纯IPv6环境App适配的坑](http://mrpeak.cn/blog/ipv6/)
* [前端技能汇总](https://github.com/JacksonTian/fks)

#CSS

```
W3C对于ID和CLASS的设定是ID具有唯一性，class具有普遍性。所以说我们用他们俩的时候就要按照这个特性
来使用。id 是不能重复的，class 却是可以重复使用，通过id可以找到页面上唯一的一个标签，而class呢
可以多个标签使用同一种样式提供了可能
```									
			
#HTML

* [HTML 5 <a> 标签的 target 属性](http://www.w3school.com.cn/html5/att_a_target.asp)

#JS
* [详解js跨域问题](https://segmentfault.com/a/1190000000718840)
* [js标准对象](http://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/00143449957099176f55ba07b764c3daa522217d0e42643000)
* [JavaScript 之 this 详解](http://www.jeffjade.com/2015/08/03/2015-08-03-javascript-this/?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io)
* [Node.js 包教不包会](https://github.com/alsotang/node-lessons)
* [vue.js 60分钟快速入门](http://www.cnblogs.com/keepfool/p/5625583.html)
* [lihei_jquery](http://blog.csdn.net/lihei12345/article/category/2393611)


## 前端

* [前端工程师手册](https://leohxj.gitbooks.io/front-end-database/content/preference/browser-rendering-performance.html)

### IDE
* [brackets](https://github.com/adobe/brackets)
* [atom](https://github.com/atom/atom)



# Python

* [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc.zh/index.html)
* [scrapy](https://github.com/scrapy/scrapy)
* [urllib3](https://github.com/shazow/urllib3)
* [requests](https://github.com/kennethreitz/requests)
* [youtube-dl](https://github.com/rg3/youtube-dl)
* [you-get](https://github.com/soimort/you-get)
* [Python的所有内置函数](https://docs.python.org/3/library/functions.html)

# DNS 
[DNS 原理入门](http://www.ruanyifeng.com/blog/2016/06/dns.html)

# Shell
* [Shell 编程初探](http://draveness.me/shell-bian-cheng-chu-tan/)
* [入门bash Shell脚本](http://blog.wtlucky.com/blog/2013/05/02/start-write-shell/)

# VPN
* [clowwindy](https://github.com/clowwindy?tab=repositories)
* [Potatso](https://github.com/shadowsocks/Potatso)
* [VPNOn](https://github.com/lexrus/VPNOn)
* [FireUpYourVPN](https://github.com/johnlui/FireUpYourVPN)





## 用telnet命令来测试服务器


