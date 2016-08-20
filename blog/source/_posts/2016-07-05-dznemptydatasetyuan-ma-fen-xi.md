---
layout: post
title: "DZNEmptyDataSet源码分析"
date: 2016-07-05 10:37:14 +0800
comments: true
categories: 
---

DZNEmptyDataSet 是一个UIscrollView的Category,用来无网络，无数据的时候显示占位图等

头文件 学习了系统tableView代理方法，有数据源(DZNEmptyDataSetSource)代理方法，与回调DZNEmptyDataSetDelegate代理方法，并且支持IB。


//常用方法
 self.tableView.emptyDataSetSource = self;
 
 内部是
 
```
- (void)setEmptyDataSetSource:(id<DZNEmptyDataSetSource>)datasource
{
     判断数据源 或者是否是 UISCrolloView或者其子类
    if (!datasource || ![self dzn_canDisplay]) {
        [self dzn_invalidate];
    }
    //运行时给 self 增加一个 DZNWeakObjectContainer 对象，并且将 datasource 作为DZNWeakObjectContainer 对象的 weak对象
    objc_setAssociatedObject(self, kEmptyDataSetSource, [[DZNWeakObjectContainer alloc] initWithWeakObject:datasource], OBJC_ASSOCIATION_RETAIN_NONATOMIC);
    
    // We add method sizzling for injecting -dzn_reloadData implementation to the native -reloadData implementation
    [self swizzleIfPossible:@selector(reloadData)];
    
    // Exclusively for UITableView, we also inject -dzn_reloadData to -endUpdates
    if ([self isKindOfClass:[UITableView class]]) {
        [self swizzleIfPossible:@selector(endUpdates)];
    }
}

```


