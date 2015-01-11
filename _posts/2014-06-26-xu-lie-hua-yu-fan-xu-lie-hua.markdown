---
layout: post
title: "序列化与反序列化"
date: 2014-06-26 15:59:06 +0800
comments: true
categories: 
---
归档即序列化与反序列化

NSCoding是一个协议，主要是下面两个方法

* -(id)initWithCoder:(NSCoder *)coder;//从coder中读取数据，保存到相应的变量中，即反序列化数据

* -(void)encoderWithCoder:(NSCoder *)coder;//读取实例变量，并把这些数据写到coder中去。

**NSCoder是一个抽象类，抽象类不能被实例化，只能提供一些想让子类继承的方法**   
**NSKeyedUnarchiver 从二进制流读取对象**   
**NSKeyedArchiver   把对象写到二进制流中去**
   
如下，在ZYRestaurant定义了如下这些属性

```

@interface ZYRestaurant : NSObject<NSCoding>

@property (nonatomic,copy) NSString *shopID;
@property (nonatomic,copy) NSString *title;
@property (nonatomic,copy) NSString *discount;
@property (nonatomic,copy) NSString *address;

@end


```

在ZYRestaurant.m里面实现如下这些方法

```
- (id)initWithCoder:(NSCoder *)aDecoder
{
    if (self = [super init]) {
        _shopID = [aDecoder decodeObjectForKey:@"shopid"];
        _title = [aDecoder decodeObjectForKey:@"title"];
        _discount = [aDecoder decodeObjectForKey:@"discount"];
        _address = [aDecoder decodeObjectForKey:@"address"];
    }
    return self;
}

- (void)encodeWithCoder:(NSCoder *)aCoder
{
    [aCoder encodeObject:self.shopID forKey:@"shopid"];
    [aCoder encodeObject:self.title forKey:@"title"];
    [aCoder encodeObject:self.discount forKey:@"discount"];
    [aCoder encodeObject:self.address forKey:@"address"];
}

```


