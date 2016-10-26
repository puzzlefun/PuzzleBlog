title: + load and + initialize
date: 2015-09-15 10:35:53
categories: iOS
tags:
- Objective-C
- iOS
description: Objective-C 中两个神奇的函数
---


<!--more-->
---------
##  + (void)load;

*The load message is sent to classes and categories that are both dynamically loaded and statically linked, but only if the newly loaded class or category implements a method that can respond.*

+load 函数是由runtime动态加载并且静态链接的，只有在自定义类中重写了才会响应load信息。+load函数的执行时机早于main函数的。在实际的项目开发中运用：

+ 初始化一些全局资源
+ 单例模式
+ 精简

\- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions

``` Objective-C
+ (void)load
{
    @autoreleasepool {
        __block id observer = [[NSNotificationCenter defaultCenter] addObserverForName:UIApplicationDidFinishLaunchingNotification object:nil queue:nil usingBlock:^(NSNotification *note) {
           //TODO you want add into the didFinishLaunchingWithOptions method
            [[NSNotificationCenter defaultCenter] removeObserver:observer];
        }];
    }
}
```

## +(void)initialize;

>
*initialize it is invoked only once per class. If you want to perform independent initialization for the class and for categories of the class, you should implement load methods.*



## Tips
Unfortunately, a load class method implemented in Swift is never called by the runtime, rendering that recommendation an impossibility.

## 引用
+ http://stackoverflow.com/questions/13326435/nsobject-load-and-initialize-what-do-they-do
+ https://www.mikeash.com/pyblog/friday-qa-2009-05-22-objective-c-class-loading-and-initialization.html
