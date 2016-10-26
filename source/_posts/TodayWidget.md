title: TodayWidget
date: 2016-01-27 16:11:14
tags:
description: containing app App extension Host App(Today)
---

<!--more-->
---------
## UI 
+ 设置最佳展示区域
```
self.preferredContentSize = CGSizeMake(self.view.bounds.size.width, 100);  
// 一般默认的View是从图标的右边开始的...如果你想变换,就要实现这个方法  
- (UIEdgeInsets)widgetMarginInsetsForProposedMarginInsets:(UIEdgeInsets)defaultMarginInsets {  
    //UIEdgeInsets newMarginInsets = UIEdgeInsetsMake(defaultMarginInsets.top, defaultMarginInsets.left - 16, defaultMarginInsets.bottom, defaultMarginInsets.right);  
    //return newMarginInsets;  
    //return UIEdgeInsetsZero; // 完全靠到了左边....  
    return UIEdgeInsetsMake(0.0, 16.0, 0, 0);  
}  
```
## Data

数据共享  App groups
```
NSUserDefaults *shared = [[NSUserDefaults alloc] initWithSuiteName:groupID]; 
NSURL *containerURL = [[NSFileManager defaultManager] containerURLForSecurityApplicationGroupIdentifier:groupID];  
containerURL = [containerURL URLByAppendingPathComponent:@"Library/Caches/test"];  
```
## Action
go to Containing App
```
[self.extensionContext openURL:[NSURL URLWithString:@"checklist://action=addlist"] completionHandler:^(BOOL success) {
        NSLog(@"add a list");
    }];
```
