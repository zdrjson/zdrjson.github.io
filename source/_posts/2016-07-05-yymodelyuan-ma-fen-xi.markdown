---
layout: post
title: "YYModel源码分析"
date: 2016-07-05 16:27:44 +0800
comments: true
categories: 
---
  总共2个类，相当tiny.
  * YYClassInfo：从类名看出关于类Class的相关信息
  * NSObject+YYModel ：NSObject的分类，意味着所有oc对象都可以有其中的方法

  
```
YYEncodingType 枚举 用来区分不同变量(第八位)、Qualifier(第8至16位)、属性(第16-24位类型)的类型、


YYClassIvarInfo
YYClassMethodInfo
YYClassPropertyInfo
YYClassInfo
```

```
NSObject+YYModel 提共的功能方法
//json ---> model
1. + (nullable instancetype)modelWithJSON:(id)json;
// Dic ---> model
2. + (nullable instancetype)modelWithDictionary:(NSDictionary *)dictionary;
// model是否是json数据转化而来
3. - (BOOL)modelSetWithJSON:(id)json;
// model是否是dic转化而来
4. - (BOOL)modelSetWithDictionary:(NSDictionary *)dic;
// model ---> json
5. - (nullable id)modelToJSONObject;
// model ---> data
6. - (nullable NSData *)modelToJSONData;
// model ---> string
7. - (nullable NSString *)modelToJSONString;
// 拷贝model
8. - (nullable id)modelCopy;
//  model序列化
9. - (void)modelEncodeWithCoder:(NSCoder *)aCoder;
// model反序列化
10. - (id)modelInitWithCoder:(NSCoder *)aDecoder;
// 得到一个modelHash code
11. - (NSUInteger)modelHash;
// 判断model是否是同一个
12. - (BOOL)modelIsEqual:(id)model; 
// model信息描述
13. - (NSString *)modelDescription; 


NSObject 分类方法就这么多，没有比较偏的，都是常用方法

接下来是Array分类方法

+ (nullable NSArray *)modelArrayWithClass:(Class)cls json:(id)json;

接下来是NSDictionary分类方法

+ (nullable NSDictionary *)modelDictionaryWithClass:(Class)cls json:(id)json;

最后是 @protocol YYModel <NSObject> 协议方法
都是可选

//设置自定义属性名
+ (nullable NSDictionary<NSString *, id> *)modelCustomPropertyMapper;

//设置容器对应的类
+ (nullable NSDictionary<NSString *, id> *)modelContainerPropertyGenericClass;

//设置自定义类名衍射属性值
+ (nullable Class)modelCustomClassForDictionary:(NSDictionary *)dictionary;

//设置属性黑名单Array，将忽略转化成model
+ (nullable NSArray<NSString *> *)modelPropertyBlacklist;

//设置属性白名单Array，如果属性不在白名单，将被忽略转化成model
+ (nullable NSArray<NSString *> *)modelPropertyWhitelist;

//与方法- (BOOL)modelCustomTransformFromDictionary:(NSDictionary *)dic;类似
//但是在model转化之前调用
- (NSDictionary *)modelCustomWillTransformFromDictionary:(NSDictionary *)dic;

//
- (BOOL)modelCustomTransformFromDictionary:(NSDictionary *)dic;
```


```
yy_modelWithJSON json转模型内部看一下内部如何调用与设计的

首先调用

+ (NSDictionary *)_yy_dictionaryWithJSON:(id)json  将json --> 字典 
因为参数是id类型，所以要先装换为json ,其中有可能是空或者字符串或者NSData
但都先转换为NSData 然后统一转换为字典
if (!json || json == (id)kCFNull) return nil;
    NSDictionary *dic = nil;
    NSData *jsonData = nil;
    if ([json isKindOfClass:[NSDictionary class]]) {
        dic = json;
    } else if ([json isKindOfClass:[NSString class]]) {
        jsonData = [(NSString *)json dataUsingEncoding : NSUTF8StringEncoding];
    } else if ([json isKindOfClass:[NSData class]]) {
        jsonData = json;
    }
    if (jsonData) {
        dic = [NSJSONSerialization JSONObjectWithData:jsonData options:kNilOptions error:NULL];
        if (![dic isKindOfClass:[NSDictionary class]]) dic = nil;
    }
    return dic;
```


```
接着是 yy_modelWithDictionary
//第一个判断是否为空
 if (!dictionary || dictionary == (id)kCFNull) return nil;
    if (![dictionary isKindOfClass:[NSDictionary class]]) return nil;
 //然后，判断是否有自定义类   
 Class cls = [self class];
    _YYModelMeta *modelMeta = [_YYModelMeta metaWithClass:cls];
    if (modelMeta->_hasCustomClassFromDictionary) {
        cls = [cls modelCustomClassForDictionary:dictionary] ?: cls;
    }
    
//没有的话 直接字典转模型
 NSObject *one = [cls new];
    if ([one yy_modelSetWithDictionary:dictionary]) return one;

其中 内部类 _YYModelMeta ,它包含类的信息model , metaWithClass 返回的是 缓存的model元类 有一个细节是字典非线程安全，所以从字典取值设值都有加锁

/// Returns the cached model class meta
+ (instancetype)metaWithClass:(Class)cls {
    if (!cls) return nil;
    static CFMutableDictionaryRef cache;
    static dispatch_once_t onceToken;
    static dispatch_semaphore_t lock;
    dispatch_once(&onceToken, ^{
        cache = CFDictionaryCreateMutable(CFAllocatorGetDefault(), 0, &kCFTypeDictionaryKeyCallBacks, &kCFTypeDictionaryValueCallBacks);
        lock = dispatch_semaphore_create(1);
    });
    dispatch_semaphore_wait(lock, DISPATCH_TIME_FOREVER);
    _YYModelMeta *meta = CFDictionaryGetValue(cache, (__bridge const void *)(cls));
    dispatch_semaphore_signal(lock);
    //meta 为空或者 meta 类需要刷新 会重新初始化 _YYModelMeta对象
    if (!meta || meta->_classInfo.needUpdate) {
        meta = [[_YYModelMeta alloc] initWithClass:cls];
        if (meta) {
            dispatch_semaphore_wait(lock, DISPATCH_TIME_FOREVER);
            CFDictionarySetValue(cache, (__bridge const void *)(cls), (__bridge const void *)(meta));
            dispatch_semaphore_signal(lock);
        }
    }
    return meta;
}



```
  

