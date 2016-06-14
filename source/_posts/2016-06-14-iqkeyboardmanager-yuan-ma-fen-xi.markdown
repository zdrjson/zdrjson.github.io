---
layout: post
title: "IQKeyboardManager 源码分析"
date: 2016-06-14 14:47:58 +0800
comments: true
categories: 
---

# 结构
 * 1.Categories 
 * 2.Constants
 * 3.IQKeyboardManager Class 核心类 单例
 * 4.IQKeyboardReturnKeyHandler Class
 * 5.IQTextView
 * 6.IQToolbar
 * 7.头文件 KeyboardManager.h
 * 8.资源目录 Resources


## 核心类 IQKeyboardManager
 
```
介绍IQKeyboardManager 无须在使用中写任何代码,任何设置 
Codeless drop-in universal library allows to prevent issues of keyboard sliding
up and cover UITextField/UITextView. Neither need to write any code nor any setup
required and much more. A generic version of KeyboardManagement. https://
developer.apple.com/Library/ios/documentation/StringsTextFonts/Conceptual/
TextAndWebiPhoneOS/KeyboardManagement/KeyboardManagement.html
```

```
/**
 Returns the default singleton instance.
 单例
 */
+ (nonnull instancetype)sharedManager;
```


```
/**
 Enable/disable managing distance between keyboard and textField. Default is YES(Enabled when class loads in `+(void)load` method).
 keyboard and textField.之间是否可用，默认可用
 */
@property(nonatomic, assign, getter = isEnabled) BOOL enable;
```


