---
layout: post
title: "MBProgressHUD"
date: 2016-06-20 14:51:30 +0800
comments: true
categories: 
---

```
- (void)show:(BOOL)animated;
- (void)hide:(BOOL)animated;
```

平时使用最多的方法之一，外部就简单的调用show或者hide，看内部如何封装的

```
- (void)show:(BOOL)animated {
  // 非主线程直接崩
    NSAssert([NSThread isMainThread], @"MBProgressHUD needs to be accessed on the main thread.");
    //记录动画flag
	useAnimation = animated;
	// If the grace time is set postpone the HUD display
	//判断是否设置时间 
	if (self.graceTime > 0.0) {
        NSTimer *newGraceTimer = [NSTimer timerWithTimeInterval:self.graceTime target:self selector:@selector(handleGraceTimer:) userInfo:nil repeats:NO];
        [[NSRunLoop currentRunLoop] addTimer:newGraceTimer forMode:NSRunLoopCommonModes];
        self.graceTimer = newGraceTimer;
	} 
	// ... otherwise show the HUD imediately 
	else {
		[self showUsingAnimation:useAnimation];
	}
}
```


```
#pragma mark - Internal show & hide operations
//内部方法
- (void)showUsingAnimation:(BOOL)animated {
    // Cancel any scheduled hideDelayed: calls
    //首先取消先前设置在HUD的selector,保证该方法不会多次调用
    [NSObject cancelPreviousPerformRequestsWithTarget:self];
    [self setNeedsDisplay];

	if (animated && animationType == MBProgressHUDAnimationZoomIn) {
		self.transform = CGAffineTransformConcat(rotationTransform, CGAffineTransformMakeScale(0.5f, 0.5f));
	} else if (animated && animationType == MBProgressHUDAnimationZoomOut) {
		self.transform = CGAffineTransformConcat(rotationTransform, CGAffineTransformMakeScale(1.5f, 1.5f));
	}
	//记录展示开始时间
	self.showStarted = [NSDate date];
	// Fade in
	if (animated) {
		[UIView beginAnimations:nil context:NULL];
		[UIView setAnimationDuration:0.30];
		self.alpha = 1.0f;
		if (animationType == MBProgressHUDAnimationZoomIn || animationType == MBProgressHUDAnimationZoomOut) {
			self.transform = rotationTransform;
		}
		[UIView commitAnimations];
	}
	else {
		self.alpha = 1.0f;
	}
}
```





## reference 
* [iOS 源代码分析 --- MBProgressHUD](https://github.com/Draveness/iOS-Source-Code-Analyze/blob/master/MBProgressHUD/iOS%20源代码分析%20---%20MBProgressHUD.md)
* [MBProgressHUD实现分析](http://southpeak.github.io/blog/2015/03/24/sourcecode-mbprogresshud/)
* [结合 Reveal 谈谈 MBProgressHUD 的用法](http://blog.leichunfeng.com/blog/2015/03/16/talking-about-the-usage-of-mbprogresshud-combined-with-reveal/)

