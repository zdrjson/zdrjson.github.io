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


```


