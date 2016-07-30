---
layout: post
title: "Masonry源码分析"
date: 2016-07-27 17:08:45 +0800
comments: true
categories: 
---

```
示例程序 常用方法 makeConstraints
[greenView makeConstraints:^(MASConstraintMaker *make) {
        make.top.greaterThanOrEqualTo(superview.top).offset(padding);
        make.left.equalTo(superview.left).offset(padding);
        make.bottom.equalTo(blueView.top).offset(-padding);
        make.right.equalTo(redView.left).offset(-padding);
        make.width.equalTo(redView.width);

        make.height.equalTo(redView.height);
        make.height.equalTo(blueView.height);
        
    }];
    
 内部调用，在View+MASShortthandAdditions 中，view的category方法
 param： 一个参数为 MASConstraintMaker实例的block
 返回值：数组
- (NSArray *)mas_makeConstraints:(void(^)(MASConstraintMaker *))block {
    //首先数组view self.translatesAutoresizingMaskIntoConstraints的属性为NO
    //为什么要设置 apple 文档中已经说明“ When you elect to position the view using auto layout by adding your own constraints, 
 you must set this property to NO. IB will do this for you.”

    self.translatesAutoresizingMaskIntoConstraints = NO;
    //创建一个MASConstraintMaker实例 把自己传进去
    MASConstraintMaker *constraintMaker = [[MASConstraintMaker alloc] initWithView:self];
    //回调block
    block(constraintMaker);
    //
    return [constraintMaker install];
}  


看一下 MASConstraintMaker 这个类，似乎挺重要
初始化方法 保存需要设置约束的view 以及 初始化约束容器
- (id)initWithView:(MAS_VIEW *)view {
    self = [super init];
    if (!self) return nil;
    
    self.view = view;
    self.constraints = NSMutableArray.new;
    
    return self;
}
@interface MASConstraintMaker : NSObject 是一个基类的约束设置器

//回到
//block(constraintMaker); 
后面会调用 下面常写的链式调用，外部调用者写起来简单，也很明了，到底里面发生？接着往下看
make.left.equalTo(superview.left).offset(padding);


make.left --- >内部是
- (MASConstraint *)left {
    return [self addConstraintWithLayoutAttribute:NSLayoutAttributeLeft];
}

接着又是调用

- (MASConstraint *)addConstraintWithLayoutAttribute:(NSLayoutAttribute)layoutAttribute {
    return [self constraint:nil addConstraintWithLayoutAttribute:layoutAttribute];
}


最终

- (MASConstraint *)constraint:(MASConstraint *)constraint addConstraintWithLayoutAttribute:(NSLayoutAttribute)layoutAttribute {
   //创建一个 MASViewAttribute 实例 ，初始化方法用 initWithView:方法
    MASViewAttribute *viewAttribute = [[MASViewAttribute alloc] initWithView:self.view layoutAttribute:layoutAttribute];
    
    //创建一个 MASViewConstraint 实例， initWithFirstViewAttribute 把上面创建个实例传入进去
    MASViewConstraint *newConstraint = [[MASViewConstraint alloc] initWithFirstViewAttribute:viewAttribute];
    //参数constraint = nil 所以不会执行下面的if
    if ([constraint isKindOfClass:MASViewConstraint.class]) {
        //replace with composite constraint
        NSArray *children = @[constraint, newConstraint];
        MASCompositeConstraint *compositeConstraint = [[MASCompositeConstraint alloc] initWithChildren:children];
        compositeConstraint.delegate = self;
        [self constraint:constraint shouldBeReplacedWithConstraint:compositeConstraint];
        return compositeConstraint;
    }
    //设置newConstraint 代理 并且添加到约束容器中
    if (!constraint) {
        newConstraint.delegate = self;
        [self.constraints addObject:newConstraint];
    }
    返回 此约束
    return newConstraint;
}


在看一下
make.top.equalTo(@20); 中 .equalTo(@20); 发生了
进MASConstraint 头文件看，make.top.equalTo就是调用:
- (MASConstraint * (^)(id attr))mas_equalTo;

具体实现

- (MASConstraint * (^)(id))mas_equalTo {
    return ^id(id attribute) {
        return self.equalToWithRelation(attribute, NSLayoutRelationEqual);
    };
}

//self.equalToWithRelation 即调用 MASViewConstraint 的父类方法
父类中已经宏定义了必须由子类实现

#define MASMethodNotImplemented() \
    @throw [NSException exceptionWithName:NSInternalInconsistencyException \
                                   reason:[NSString stringWithFormat:@"You must override %@ in a subclass.", NSStringFromSelector(_cmd)] \
                                 userInfo:nil]
                                 
                                 
                                 
                                 
具体实现

#pragma mark - NSLayoutRelation proxy

- (MASConstraint * (^)(id, NSLayoutRelation))equalToWithRelation {
    return ^id(id attribute, NSLayoutRelation relation) {
        //不是属性数组进入else
        if ([attribute isKindOfClass:NSArray.class]) {
            NSAssert(!self.hasLayoutRelation, @"Redefinition of constraint relation");
            NSMutableArray *children = NSMutableArray.new;
            for (id attr in attribute) {
                MASViewConstraint *viewConstraint = [self copy];
                viewConstraint.secondViewAttribute = attr;
                [children addObject:viewConstraint];
            }
            MASCompositeConstraint *compositeConstraint = [[MASCompositeConstraint alloc] initWithChildren:children];
            compositeConstraint.delegate = self.delegate;
            [self.delegate constraint:self shouldBeReplacedWithConstraint:compositeConstraint];
            return compositeConstraint;
        } else {
        
            NSAssert(!self.hasLayoutRelation || self.layoutRelation == relation && [attribute isKindOfClass:NSValue.class], @"Redefinition of constraint relation");
            self.layoutRelation = relation;
            self.secondViewAttribute = attribute;
            return self;
        }
    };
}
   





```


