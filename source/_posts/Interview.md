title: Interview
date: 2015-12-10 09:58:51
categories: iOS
tags: 
- Objective-C 
description: 反思在反思，学习iOS已经好一段时间了，不知道能不能找到工作，已是问问大牛一般面试都会考察一些什么问题。以下就是向大牛学习以及自己平时思考的问题。
---

面试的过程除了考察项目经历外，还会着重考察基础知识
程序员面试除了问问数据结构、算法还能问点什么呢？
<!--more-->
---------
### 1 Objective-C 的内存管理模型？
MRC(retain, realse) ==》 ARC(strong, weak, copy, assign)
引用计数模型

### 2 autorealse

### 3 NSString 变量的赋值 是否共用同一份内存
NSString && NSMutabeString
```
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        
        NSString *hello = @"hello world";
        NSString *world = hello;
        NSLog(@"1. %p =? %p", hello, world);
        NSString *hi = @"hello world";
        NSLog(@"2. %p =? %p",hello, hi);
        NSString *hei = [NSString stringWithFormat:@"%@", @"hello world"]; 
        NSLog(@"3. %p =? %p", hello, hei); //采用类实例化的常量字符串是不同的对象
        
        NSMutableString *mutableHello = [NSMutableString stringWithString:hello];
        NSLog(@"4. %p =? %p", hello, mutableHello);
        NSString *hellocopy = [hello copy];
        NSLog(@"5. %p =? %p", hello, hellocopy); //同一个对象的两份引用
        NSMutableString *helloMutableCopy = [hello mutableCopy];
        NSLog(@"6. %p =? %p", hello, helloMutableCopy); //终于产生新对象了
        
        NSString *mutableHelloCopy = [mutableHello copy];
        NSLog(@"7. %p =? %p", mutableHello, mutableHelloCopy); //我们都是新对象
        NSString *mutableHelloMutableCopy = [mutableHello mutableCopy];
        NSLog(@"8. %p =? %p", mutableHello, mutableHelloMutableCopy); //我们都是新对象
        
    }
    return 0;
}

/*
2015-12-10 10:32:32.098 Interview[3940:264604] 1. 0x100001048 =? 0x100001048
2015-12-10 10:32:32.099 Interview[3940:264604] 2. 0x100001048 =? 0x100001048
2015-12-10 10:32:32.099 Interview[3940:264604] 3. 0x100001048 =? 0x1007000e0
2015-12-10 10:32:32.099 Interview[3940:264604] 4. 0x100001048 =? 0x1007000a0
2015-12-10 10:32:32.099 Interview[3940:264604] 5. 0x100001048 =? 0x100001048
2015-12-10 10:32:32.099 Interview[3940:264604] 6. 0x100001048 =? 0x1007002a0
2015-12-10 10:32:32.099 Interview[3940:264604] 7. 0x1007000a0 =? 0x1001067f0
2015-12-10 10:32:32.099 Interview[3940:264604] 8. 0x1007000a0 =? 0x100106810
Program ended with exit code: 0
*/

```
NSArrary && NSMutableArrary 
```
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        NSArray * array = @[@1, @2];
        NSArray * arrayCopy = [array copy];
        NSArray * arrayMutableCopy = [array mutableCopy];
        NSArray * arrayDeepCopy = [[NSArray alloc] initWithArray:array copyItems:YES];
        NSLog(@" array = %p",array);
        NSLog(@" arrayCopy = %p",arrayCopy); // I am s shadow
        NSLog(@" arrayMutableCopy = %p",arrayMutableCopy);
        NSLog(@" arrayDeepCopy = %p",arrayDeepCopy);
        
        NSMutableArray * mutableArray = [NSMutableArray arrayWithArray:array];
        NSMutableArray * mutableArrayCopy = [array copy];
        NSMutableArray * mutableArrayMutableCopy = [array mutableCopy];
        NSMutableArray * mutableArrayDeepCopy = [[NSMutableArray alloc] initWithArray:array copyItems:YES];
        NSLog(@" mutableArray = %p",mutableArray);
        NSLog(@" mutableArrayCopy = %p",mutableArrayCopy);
        NSLog(@" mutableArrayMutableCopy = %p",mutableArrayMutableCopy);
        NSLog(@" mutableArrayDeepCopy = %p",mutableArrayDeepCopy);
    }
    return 0;
}
/*
2015-12-10 14:15:44.061 Interview[4386:341668]  array = 0x100106d30
2015-12-10 14:15:44.062 Interview[4386:341668]  arrayCopy = 0x100106d30
2015-12-10 14:15:44.062 Interview[4386:341668]  arrayMutableCopy = 0x1001069f0
2015-12-10 14:15:44.062 Interview[4386:341668]  arrayDeepCopy = 0x100106da0
2015-12-10 14:15:44.063 Interview[4386:341668]  mutableArray = 0x100201490
2015-12-10 14:15:44.063 Interview[4386:341668]  mutableArrayCopy = 0x100106d30
2015-12-10 14:15:44.063 Interview[4386:341668]  mutableArrayMutableCopy = 0x100203d80
2015-12-10 14:15:44.063 Interview[4386:341668]  mutableArrayDeepCopy = 0x1002037f0
Program ended with exit code: 0
*/

```
NSDictionary && NSMutableDictionary

### 4 copy 属性的作用
### 5 什么是runtime
面向对象  动态语言 消息传递

```
OBJC_EXPORT void objc_msgSend(void /* id self, SEL op, ... */ )
    __OSX_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
	
+ (BOOL)resolveClassMethod:(SEL)sel __OSX_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
+ (BOOL)resolveInstanceMethod:(SEL)sel __OSX_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);

- (id)forwardingTargetForSelector:(SEL)aSelector __OSX_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);

- (NSMethodSignature *)methodSignatureForSelector:(SEL)aSelector OBJC_SWIFT_UNAVAILABLE("");
```
程序的执行逻辑在运行时 动态绑定
### 6 什么情况下产生引用循环，以及如何避免 
```
#import <Foundation/Foundation.h>

@interface AObject : NSObject
- (void)setupEnv;
@end

@protocol CDelegate <NSObject>
@optional
- (void)sayhello;
@end

@interface BObject : NSObject
@property (nonatomic, strong) id<CDelegate> delegate;
@end

@interface AObject () <CDelegate>
@property (nonatomic, strong) BObject *b;
@property (nonatomic, copy) void (^hi)();
@property (nonatomic, copy) NSString *name;
@end

@implementation AObject

- (void)setupEnv {
    self.b = [[BObject alloc] init];
    self.b.delegate = self; // cycle one
    self.name = @"hello world";
    __weak typeof(self) weakSelf = self; //什么时候可能导致weakSelf == nil ?
    self.hi = ^() {
        NSLog(@"slef == %@", weakSelf); // cycle two?
        NSLog(@"%@", weakSelf.name);
    };   
}
@end

```
## 引用
【1】http://stackoverflow.com/questions/27152580/cocoa-blocks-as-strong-pointers-vs-copy

