title: Crash
date: 2016-02-02 14:42:01
ico: fa-bug
tags:
- Crash
keywords: Crash, iOS
description: 今天App又Crash了吗？导致Crash的原因可能很多，同样分析Crash的手段也很多，我们来缕缕看。
-----

## 解析Crash准备的材料
+ 原材料：Crash log 
+ 辅料： dysm 和 app
+ 工具： symbolicatecrash, otool, xcrun, atos


## 收集材料
+ （Xcode）Windows -> Device -> View Device Logs 
+  Log 收集第三方平台
+  打包应用时的 .xcarchive(dysm, app)

## 第一道菜 Symbolicatecrash
``` shell
find /Applications/Xcode.app -name symbolicatecrash -type f

/Applications/Xcode.app/Contents/SharedFrameworks/DTDeviceKitBase.framework/Versions/A/Resources/symbolicatecrash
```

## 分析
```
/Applications/Xcode.app/Contents/SharedFrameworks/DTDeviceKitBase.framework/Versions/A/Resources/symbolicatecrash 56ae4a1e0feaad87628b4c8e.crash ThumbDoctor.app.dSYM > crash.txt

---
## Warning: Unable to symbolicate from required binary: /Users/lkeg/Library/Developer/Xcode/iOS DeviceSupport/8.3 (12F70)/Symbols/System/Library/Frameworks/CoreLocation.framework/CoreLocation
---

出现
----
Error: "DEVELOPER_DIR" is not defined at /Applications/Xcode.app/Contents/SharedFrameworks/DTDeviceKitBase.framework/Versions/A/Resources/symbolicatecrash line 60.
----

export DEVELOPER_DIR="/Applications/XCode.app/Contents/Developer"
```
## 第二道菜 符号地址逐行解析
起始地址：即使每次iOS app启动都会加载(main module)主模块在不同的内存地址（大多数情况下32bit框架对应的地址是0x4000、64bit框架对应的地址为0x0000000100000000）。
+ cd xx.app
+ 
``` llvm
     otool -arch arm64 -l xxx.app/xxx  | grep -B 1 -A 10 "LC_SEGM" | grep -B 3 -A 8 "__TEXT"
     
     Load command 1
      cmd LC_SEGMENT_64
  cmdsize 952
  segname __TEXT
   vmaddr 0x0000000100000000
   vmsize 0x00000000000b8000
  fileoff 0
 filesize 753664
  maxprot 0x00000005
 initprot 0x00000005
   nsects 11
    flags 0x0
```
其中 vmaddr 0x0000000100000000 地址便为我们所要的app运行起始地址。

### 计算 symbol address 
symbol address = 地址偏移量＋起始地址。
起始地址上面我们已经得到，地址偏移量就是单行信息中“+”号后面的数值。

### 解析 symbol address 
xcrun atos --arch arm64 -o xxx.app/xxx [addresss]

### load address 相对偏移解析

xcrun atos --arch arm64 -o xxx.app/xxx -l [address] [address]


## reference
+ https://www.plcrashreporter.org/
