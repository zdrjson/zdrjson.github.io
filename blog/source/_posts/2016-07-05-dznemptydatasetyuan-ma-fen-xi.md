---
layout: post
title: "DZNEmptyDataSet源码分析"
date: 2016-07-05 10:37:14 +0800
comments: true
categories: 
---

DZNEmptyDataSet 是一个UIscrollView的Category,用来无网络，无数据的时候显示占位图等

头文件 学习了系统tableView代理方法，有数据源(DZNEmptyDataSetSource)代理方法，与回调DZNEmptyDataSetDelegate代理方法，并且支持IB。
头文件非常清晰，值得学习。

//无网络占位图，


//常用方法
 self.tableView.emptyDataSetSource = self;
 
 内部是
 
```
//设置数据源代理
- (void)setEmptyDataSetSource:(id<DZNEmptyDataSetSource>)datasource
{
     判断数据源 或者是否是 UISCrolloView或者其子类
    if (!datasource || ![self dzn_canDisplay]) {
        [self dzn_invalidate];
    }
    //运行时给 self 增加一个 DZNWeakObjectContainer 对象，并且将 datasource 作为DZNWeakObjectContainer 对象的 weak对象
    objc_setAssociatedObject(self, kEmptyDataSetSource, [[DZNWeakObjectContainer alloc] initWithWeakObject:datasource], OBJC_ASSOCIATION_RETAIN_NONATOMIC);
    
    // We add method sizzling for injecting -dzn_reloadData implementation to the native -reloadData implementation
    //替换原生的reload  方法
    [self swizzleIfPossible:@selector(reloadData)];
    
    //如果是tableView 则 注入endUpdates 到 dzn_reloadData
    // Exclusively for UITableView, we also inject -dzn_reloadData to -endUpdates
    if ([self isKindOfClass:[UITableView class]]) {
        [self swizzleIfPossible:@selector(endUpdates)];
    }
}

```

//交互方法实现 实际就是 后面调用reload 会调用 dzn_reloadEmptyDataSet 方法
- (void)swizzleIfPossible:(SEL)selector
{
    // Check if the target responds to selector
    //检查self是否能响应这个selector
    if (![self respondsToSelector:selector]) {
        return;
    }
    //创建查找字典
    // Create the lookup table
    if (!_impLookupTable) {
        _impLookupTable = [[NSMutableDictionary alloc] initWithCapacity:3]; // 3 represent the supported base classes
    }
    
    // We make sure that setImplementation is called once per class kind, UITableView or UICollectionView.
    for (NSDictionary *info in [_impLookupTable allValues]) {
        Class class = [info objectForKey:DZNSwizzleInfoOwnerKey];
        NSString *selectorName = [info objectForKey:DZNSwizzleInfoSelectorKey];
        
        if ([selectorName isEqualToString:NSStringFromSelector(selector)]) {
            if ([self isKindOfClass:class]) {
                return;
            }
        }
    }
    
    Class baseClass = dzn_baseClassToSwizzleForTarget(self);
    NSString *key = dzn_implementationKey(baseClass, selector);
    NSValue *impValue = [[_impLookupTable objectForKey:key] valueForKey:DZNSwizzleInfoPointerKey];
    
    // If the implementation for this class already exist, skip!!
    if (impValue || !key || !baseClass) {
        return;
    }
    
    // Swizzle by injecting additional implementation
    Method method = class_getInstanceMethod(baseClass, selector);
//    printf("method - %@\n",method);
    IMP dzn_newImplementation = method_setImplementation(method, (IMP)dzn_original_implementation);
//    printf("dzn_newImplementation- %@\n",dzn_newImplementation);
    
    // Store the new implementation in the lookup table
    NSDictionary *swizzledInfo = @{DZNSwizzleInfoOwnerKey: baseClass,
                                   DZNSwizzleInfoSelectorKey: NSStringFromSelector(selector),
                                   DZNSwizzleInfoPointerKey: [NSValue valueWithPointer:dzn_newImplementation]};
    NSLog(@"swizzledInfo %@",swizzledInfo);
    [_impLookupTable setObject:swizzledInfo forKey:key];
}

  其中dzn_baseClassToSwizzleForTarget 会多次调用,可以增加缓存类似下面这样
  
``` 
  static Class class = nil;
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        if ([target isKindOfClass:[UITableView class]]) {
            class =  [UITableView class];
        }
        else if ([target isKindOfClass:[UICollectionView class]]) {
            class = [UICollectionView class];
        }
        else if ([target isKindOfClass:[UIScrollView class]]) {
            class = [UIScrollView class];
        }
    });
    return class;
```

