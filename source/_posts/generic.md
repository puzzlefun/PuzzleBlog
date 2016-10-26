title: Generic
date: 2015-12-11 14:01:26
categories: iOS
tags: 
- Objective-C 
description: 拥抱泛型
---

<!--more-->
---------
``` 
//C++ 

@protocol Barking <NSObject>

- (void)bark;

@end

//template
@interface Animal<AnyObject, AnyObject2>:NSObject

@end

@class Dog;

//instance
@interface Dog : Animal<Dog *, NSString *> <Barking>//protocol

@end

```