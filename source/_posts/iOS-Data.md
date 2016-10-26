title: iOS-Data
date: 2015-10-19 19:28:06
categories: iOS
tags: iOS
description: 数据是最重要的
---

<!--more-->
---------
Mantle FMDB

App 沙盒(sandbox)

+ ./application
+ + Document [syn]
+ + Library
+ | +   Caches
  | +   Preferences [syn]
+ + tmp

``` Objective-C

NSString *homeDirectory = NSHomeDirectory();  //沙盒根目录
NSArray *paths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);  
NSString *documnet = paths.firstObject;
NSArray *paths = NSSearchPathForDirectoriesInDomains(NSLibraryDirectory, NSUserDomainMask, YES);  
NSString *library = paths.firstObject;
NSString *tmpDir = NSTemporaryDirectory();
NSArray *paths = NSSearchPathForDirectoriesInDomains(NSCachesDirectory, NSUserDomainMask, YES);  
NSString *caches = paths.firstObject;
NSBundle *applicationBundle = [NSBundle mainBundle];
NSString *path = [applicationBundle pathForResource:@"myfile" ofType:@"type"];

NSFileManager *fileManager = [NSFileManager defaultManager];

```

-

+ http://nshipster.com/nsfilemanager/

-

# NSuserDefaults

*基础类型，NSString, NSData, NSArrary, NSDictory, NSURL*

# plist
*A property list is a representation of a hierarchy of objects that can be stored in the file system and reconstituted later. Property lists give applications a lightweight and portable way to store small amounts of data.*

``` Objective-C
//NSDictory 
- (nullable NSDictionary<KeyType, ObjectType> *)initWithContentsOfFile:(NSString *)path;
//NSArrary NSData
- (BOOL)writeToFile:(NSString *)path atomically:(BOOL)useAuxiliaryFile;
... ...
```