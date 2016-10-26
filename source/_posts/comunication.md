title: Comunication
date: 2016-01-26 14:59:28
tags:
description: 本文主要分析移动开发中，不同端的通信方式，以及推荐最佳的Mobile First的设计建议
---

## URL Scheme
完整的：
scheme://user:password@host:port/path?query#fragment
简化的：
scheme://host/path?query

NSURL
NSURLComponents
@interface NSString (NSURLUtilities)

// Returns a new string made from the receiver by replacing all characters not in the allowedCharacters set with percent encoded characters. UTF-8 encoding is used to determine the correct percent encoded characters. Entire URL strings cannot be percent-encoded. This method is intended to percent-encode an URL component or subcomponent string, NOT the entire URL string. Any characters in allowedCharacters outside of the 7-bit ASCII range are ignored.
- (nullable NSString *)stringByAddingPercentEncodingWithAllowedCharacters:(NSCharacterSet *)allowedCharacters NS_AVAILABLE(10_9, 7_0);

// Returns a new string made from the receiver by replacing all percent encoded sequences with the matching UTF-8 characters.
@property (nullable, readonly, copy) NSString *stringByRemovingPercentEncoding NS_AVAILABLE(10_9, 7_0);


- (nullable NSString *)stringByAddingPercentEscapesUsingEncoding:(NSStringEncoding)enc NS_DEPRECATED(10_0, 10_11, 2_0, 9_0, "Use -stringByAddingPercentEncodingWithAllowedCharacters: instead, which always uses the recommended UTF-8 encoding, and which encodes for a specific URL component or subcomponent since each URL component or subcomponent has different rules for what characters are valid.");
- (nullable NSString *)stringByReplacingPercentEscapesUsingEncoding:(NSStringEncoding)enc NS_DEPRECATED(10_0, 10_11, 2_0, 9_0, "Use -stringByRemovingPercentEncoding instead, which always uses the recommended UTF-8 encoding.");

@end

App 之间Comunication
设置 
plist
发送
```
// UIApplication
- (BOOL)openURL:(NSURL*)url NS_EXTENSION_UNAVAILABLE_IOS("");
- (BOOL)canOpenURL:(NSURL *)url NS_AVAILABLE_IOS(3_0)
```
接受
```
// UIApplicationDelegate
- (BOOL)application:(UIApplication *)application handleOpenURL:(NSURL *)url NS_DEPRECATED_IOS(2_0, 9_0, "Please use application:openURL:options:") __TVOS_PROHIBITED;
- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(nullable NSString *)sourceApplication annotation:(id)annotation NS_DEPRECATED_IOS(4_2, 9_0, "Please use application:openURL:options:") __TVOS_PROHIBITED;
- (BOOL)application:(UIApplication *)app openURL:(NSURL *)url options:(NSDictionary<NSString*, id> *)options NS_AVAILABLE_IOS(9_0); // no equiv. notification. return NO if the application can't open for some reason
```
### refer
+ http://iosdevelopertips.com/cocoa/launching-your-own-application-via-a-custom-url-scheme.html
+ https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html


## Universal Links

设置
web
---
1 创建 apple-app-site-association 配置文件（没有后缀），文件内包含App可以处理的JSON格式URLs设置
2 上传 apple-app-site-association 文件至HTTPS服务器
3 App完成处理 universal links 编码

实例
{
    "applinks": {
        "apps": [],
        "details": [
            {
                "appID": "9JA89QQLNQ.com.apple.wwdc",
                "paths": [ "/wwdc/news/", "/videos/wwdc/2015/*"]
            },
            {
                "appID": "TeamID.BundleID2",
                "paths": [ "*" ]
            }
        ]
    }
}

App
---
Add an entitlement that specifies the domains your app supports.
Update your app delegate to respond appropriately when it receives the NSUserActivity object.
NSUserActivityTypeBrowsingWeb
```
// Called on the main thread after the NSUserActivity object is available. Use the data you stored in the NSUserActivity object to re-create what the user was doing.
// You can create/fetch any restorable objects associated with the user activity, and pass them to the restorationHandler. They will then have the UIResponder restoreUserActivityState: method
// invoked with the user activity. Invoking the restorationHandler is optional. It may be copied and invoked later, and it will bounce to the main thread to complete its work and call
// restoreUserActivityState on all objects.
- (BOOL)application:(UIApplication *)application continueUserActivity:(NSUserActivity *)userActivity restorationHandler:(void(^)(NSArray * __nullable restorableObjects))restorationHandler NS_AVAILABLE_IOS(8_0);
```

## relation
HandOff
Core Spotlight

### refer
+ https://developer.apple.com/library/prerelease/ios/documentation/General/Conceptual/AppSearch/UniversalLinks.html
