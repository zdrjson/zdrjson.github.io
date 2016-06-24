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


```
- (void)hide:(BOOL)animated {
    //判断是否在主线程 非主线程直接崩
    NSAssert([NSThread isMainThread], @"MBProgressHUD needs to be accessed on the main thread.");
	useAnimation = animated;
	// If the minShow time is set, calculate how long the hud was shown,
	// and pospone the hiding operation if necessary
	//如果设置了最短展示时间，先比较展示到现在的时间与最短时间,如果前者小设置self.minShowTimer(有什么用？)，然后返回，在 (self.minShowTime - interv)差值时间后 执行
		[self hideUsingAnimation:useAnimation];
		
	if (self.minShowTime > 0.0 && showStarted) {
		NSTimeInterval interv = [[NSDate date] timeIntervalSinceDate:showStarted];
		if (interv < self.minShowTime) {
			self.minShowTimer = [NSTimer scheduledTimerWithTimeInterval:(self.minShowTime - interv) target:self 
								selector:@selector(handleMinShowTimer:) userInfo:nil repeats:NO];
			return;
		} 
	}
	// ... otherwise hide the HUD immediately
	[self hideUsingAnimation:useAnimation];
}
```

//隐藏主方法
```
- (void)hideUsingAnimation:(BOOL)animated {
	// Fade out
	if (animated && showStarted) {
		[UIView beginAnimations:nil context:NULL];
		[UIView setAnimationDuration:0.30];
		[UIView setAnimationDelegate:self];
		[UIView setAnimationDidStopSelector:@selector(animationFinished:finished:context:)];
		// 0.02 prevents the hud from passing through touches during the animation the hud will get completely hidden
		// in the done method
		if (animationType == MBProgressHUDAnimationZoomIn) {
			self.transform = CGAffineTransformConcat(rotationTransform, CGAffineTransformMakeScale(1.5f, 1.5f));
		} else if (animationType == MBProgressHUDAnimationZoomOut) {
			self.transform = CGAffineTransformConcat(rotationTransform, CGAffineTransformMakeScale(0.5f, 0.5f));
		}

		self.alpha = 0.02f;
		[UIView commitAnimations];
	}
	else {
		self.alpha = 0.0f;
		//主要这行代码
		[self done];
	}
	//清空showStarted
	self.showStarted = nil;
}
```

```
- (void)done {
	[NSObject cancelPreviousPerformRequestsWithTarget:self];
	//清空
	isFinished = YES;
	self.alpha = 0.0f;
	if (removeFromSuperViewOnHide) {
		[self removeFromSuperview];
	}
	//回调block与delegate,但得先判断
#if NS_BLOCKS_AVAILABLE
	if (self.completionBlock) {
		self.completionBlock();
		self.completionBlock = NULL;
	}
#endif
	if ([delegate respondsToSelector:@selector(hudWasHidden:)]) {
		[delegate performSelector:@selector(hudWasHidden:) withObject:self];
	}
}
```


### 关于自定义label或者detailLabel属性,作者用了KVO

```
#pragma mark - KVO

- (void)registerForKVO {
	for (NSString *keyPath in [self observableKeypaths]) {
		[self addObserver:self forKeyPath:keyPath options:NSKeyValueObservingOptionNew context:NULL];
	}
}

- (void)unregisterFromKVO {
	for (NSString *keyPath in [self observableKeypaths]) {
		[self removeObserver:self forKeyPath:keyPath];
	}
}

- (NSArray *)observableKeypaths {
	return [NSArray arrayWithObjects:@"mode", @"customView", @"labelText", @"labelFont", @"labelColor",
			@"detailsLabelText", @"detailsLabelFont", @"detailsLabelColor", @"progress", @"activityIndicatorColor", nil];
}

- (void)observeValueForKeyPath:(NSString *)keyPath ofObject:(id)object change:(NSDictionary *)change context:(void *)context {
	if (![NSThread isMainThread]) {
		[self performSelectorOnMainThread:@selector(updateUIForKeypath:) withObject:keyPath waitUntilDone:NO];
	} else {
		[self updateUIForKeypath:keyPath];
	}
}

- (void)updateUIForKeypath:(NSString *)keyPath {
	if ([keyPath isEqualToString:@"mode"] || [keyPath isEqualToString:@"customView"] ||
		[keyPath isEqualToString:@"activityIndicatorColor"]) {
		[self updateIndicators];
	} else if ([keyPath isEqualToString:@"labelText"]) {
		label.text = self.labelText;
	} else if ([keyPath isEqualToString:@"labelFont"]) {
		label.font = self.labelFont;
	} else if ([keyPath isEqualToString:@"labelColor"]) {
		label.textColor = self.labelColor;
	} else if ([keyPath isEqualToString:@"detailsLabelText"]) {
		detailsLabel.text = self.detailsLabelText;
	} else if ([keyPath isEqualToString:@"detailsLabelFont"]) {
		detailsLabel.font = self.detailsLabelFont;
	} else if ([keyPath isEqualToString:@"detailsLabelColor"]) {
		detailsLabel.textColor = self.detailsLabelColor;
	} else if ([keyPath isEqualToString:@"progress"]) {
		if ([indicator respondsToSelector:@selector(setProgress:)]) {
			[(id)indicator setValue:@(progress) forKey:@"progress"];
		}
		return;
	}
	[self setNeedsLayout];
	[self setNeedsDisplay];
}

```


## reference 
* [iOS 源代码分析 --- MBProgressHUD](https://github.com/Draveness/iOS-Source-Code-Analyze/blob/master/MBProgressHUD/iOS%20源代码分析%20---%20MBProgressHUD.md)
* [MBProgressHUD实现分析](http://southpeak.github.io/blog/2015/03/24/sourcecode-mbprogresshud/)
* [结合 Reveal 谈谈 MBProgressHUD 的用法](http://blog.leichunfeng.com/blog/2015/03/16/talking-about-the-usage-of-mbprogresshud-combined-with-reveal/)

