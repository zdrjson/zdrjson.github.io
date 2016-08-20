---
layout: post
title: "FDFullscreenPopGesture 源码分析"
date: 2016-08-10 19:58:57 +0800
comments: true
categories: 
---

需求：大屏手机要求更多用户要求导航控制器全屏手势返回，而不满足原生的左侧一小段系统手势返回
code: 导航控制器的分类

具体实现：

```
在 load 方法中 交互导航控制器的 pushViewController:animated: 方法
+ (void)load
{
    // Inject "-pushViewController:animated:"
    Method originalMethod = class_getInstanceMethod(self, @selector(pushViewController:animated:));
    Method swizzledMethod = class_getInstanceMethod(self, @selector(fd_pushViewController:animated:));
    method_exchangeImplementations(originalMethod, swizzledMethod);
}


//自己实现交换后的 pushViewController:animated: 
- (void)fd_pushViewController:(UIViewController *)viewController animated:(BOOL)animated
{
  //首先判断导航控制器手势view中的gestureRecognizers  数组是否包含自己添加的全屏手势Recognizer
    if (![self.interactivePopGestureRecognizer.view.gestureRecognizers containsObject:self.fd_fullscreenPopGestureRecognizer]) {
        
        // Add our own gesture recognizer to where the onboard screen edge pan gesture recognizer is attached to.
        //导航控制器手势view中的gestureRecognizers  数组增加  自己添加的全屏手势Recognizer
        [self.interactivePopGestureRecognizer.view addGestureRecognizer:self.fd_fullscreenPopGestureRecognizer];

        // Forward the gesture events to the private handler of the onboard gesture recognizer.
        NSArray *internalTargets = [self.interactivePopGestureRecognizer valueForKey:@"targets"];
        id internalTarget = [internalTargets.firstObject valueForKey:@"target"];
        SEL internalAction = NSSelectorFromString(@"handleNavigationTransition:");
        self.fd_fullscreenPopGestureRecognizer.delegate = self.fd_popGestureRecognizerDelegate;
        [self.fd_fullscreenPopGestureRecognizer addTarget:internalTarget action:internalAction];

        // Disable the onboard gesture recognizer.
        self.interactivePopGestureRecognizer.enabled = NO;
    }
    
    // Handle perferred navigation bar appearance.
    [self fd_setupViewControllerBasedNavigationBarAppearanceIfNeeded:viewController];
    
    // Forward to primary implementation.
    [self fd_pushViewController:viewController animated:animated];
}


```


