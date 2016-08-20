---
layout: post
title: "SVProgressHUD源码阅读"
date: 2016-06-27 19:10:50 +0800
comments: true
categories: 
---

 首先看一下SVProgressHUD结构，4个类
  SVProgressHUD 核心类，头文件都是类方法,继承UIView
  SVProgressAnimatedView 与 SVProgressAnimatedView 是动画View
  SVRadialGradientLayer 是Calayer 子类 ，只有一个属性设置 gradientCenter
 
 

  平时写的最多方法之一
  
  ```
  + (void)show;
  ```

  其内部调用
  
  ```
  + (void)showWithStatus:(NSString*)status {
    //初始化 svp对象，为单例对象，其中 SV_APP_EXTENSIONS 是为了在App Extensions中使用svp，防止Api不可用,单例中要注意：SVProgressHUD对象是全屏的
    [self sharedView];
    [self showProgress:SVProgressHUDUndefinedProgress status:status];
  }
  ```
  
 
```
  [self showProgress:SVProgressHUDUndefinedProgress status:status];
```
  上面这个方法最后会调用到下面的方法
  
```
#pragma mark - Master show/dismiss methods

- (void)showProgress:(float)progress status:(NSString*)status {
    __weak SVProgressHUD *weakSelf = self;
    // 不管在不在主线程，直接回到主线程
    [[NSOperationQueue mainQueue] addOperationWithBlock:^{
        __strong SVProgressHUD *strongSelf = weakSelf;
        if(strongSelf){
            //更新检测view的层次确保HUD可视
            // Update / Check view hierachy to ensure the HUD is visible
            //下面会说
            [strongSelf updateViewHierachy];
            
            // Reset imageView and fadeout timer if an image is currently displayed
            //第一次初始化 self.imageView以及 父View self.hudView
            strongSelf.imageView.hidden = YES;
            strongSelf.imageView.image = nil;
            
            if(strongSelf.fadeOutTimer) {
                strongSelf.activityCount = 0;
            }
            strongSelf.fadeOutTimer = nil;
            
            // Update text and set progress to the given value
            strongSelf.statusLabel.text = status;
            strongSelf.progress = progress;
            
            // Choose the "right" indicator depending on the progress
            if(progress >= 0) {
                // Cancel the indefiniteAnimatedView, then show the ringLayer
                [strongSelf cancelIndefiniteAnimatedViewAnimation];
                
                // Add ring to HUD and set progress
                [strongSelf.hudView addSubview:strongSelf.ringView];
                [strongSelf.hudView addSubview:strongSelf.backgroundRingView];
                strongSelf.ringView.strokeEnd = progress;
                
                // Updat the activity count
                if(progress == 0) {
                    strongSelf.activityCount++;
                }
            } else {
                // Cancel the ringLayer animation, then show the indefiniteAnimatedView
                [strongSelf cancelRingLayerAnimation];
                
                // Add indefiniteAnimatedView to HUD
                [strongSelf.hudView addSubview:strongSelf.indefiniteAnimatedView];
                if([strongSelf.indefiniteAnimatedView respondsToSelector:@selector(startAnimating)]) {
                    [(id)strongSelf.indefiniteAnimatedView startAnimating];
                }
                
                // Update the activity count
                strongSelf.activityCount++;
            }
            
            // Show
            [strongSelf showStatus:status];
        }
    }];
}

```


```
 [strongSelf updateViewHierachy];
 会调用
 
 - (void)updateViewHierachy {
    // Add the overlay (e.g. black, gradient) to the application window if necessary
    if(!self.overlayView.superview) {
#if !defined(SV_APP_EXTENSIONS)
        // Default case: iterate over UIApplication windows
        NSEnumerator *frontToBackWindows = [UIApplication.sharedApplication.windows reverseObjectEnumerator];
        //reverseObjectEnumerator 数组反序
        

        
        for (UIWindow *window in frontToBackWindows) {
            NSLog(@"%@",window);
            BOOL windowOnMainScreen = window.screen == UIScreen.mainScreen;
            BOOL windowIsVisible = !window.hidden && window.alpha > 0;
            BOOL windowLevelNormal = window.windowLevel == UIWindowLevelNormal;
            NSLog(@"%d",UIWindowLevelNormal);
            NSLog(@"%d",window.windowLevel);
            NSLog(@"%d",windowLevelNormal);
            if(windowOnMainScreen && windowIsVisible && windowLevelNormal) {
                [window addSubview:self.overlayView];
                break;
            }
        }
#else
        // If SVProgressHUD ist used inside an app extension add it to the given view
        if(self.viewForExtension) {
            [self.viewForExtension addSubview:self.overlayView];
        }
#endif
    } else {
        // The HUD is already on screen, but maybot not in front. Therefore
        // ensure that overlay will be on top of rootViewController (which may
        // be changed during runtime).
        [self.overlayView.superview bringSubviewToFront:self.overlayView];
    }
    
    
    // Add self to the overlay view
    if(!self.superview){
        [self.overlayView addSubview:self];
    }
    if(!self.hudView.superview) {
        [self addSubview:self.hudView];
    }
   最后形成
   window add self.overlayview 
   self.overlayview add self
   self add self.hud
   // widnow、 self.overlayview、self 的frame 为全屏
   //self.hud frame 为 CGRectZero 
}
 
 
 
```
  
## 小结
SVProgress:




