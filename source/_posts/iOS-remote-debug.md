---
title: 构建iOS 远程调试环境
date: 2016-09-21 15:07:28
tags:
- iOS 
- lldb 
---

预备环境：
macOS jailbreak iOS 

1 拷贝debugserver 至Mac 本地
```
scp root@{iOS ip}:/Developer/usr/bin/debugserver ~/debugserver
lipo -thin arm64 ~/debugserver -output ~/debugserver

```
2 给debugserver 添加 task_for_pid 权限
新建文件 ent.xml
```
<plist version="1.0">
<dict>
<key>com.apple.springboard.debugapplications</key>
<true/>
<key>get-task-allow</key>
<true/>
<key>task_for_pid-allow</key>
<true/>
<key>run-unsigned-code</key>
<true/>
</dict>
</plist>
```
```
ldid -Sent.xml debugserver
```

3 将处理过后的 debugserver 拷贝会 iOS 
```
scp ~/debugserver root@{iOS ip}:/usr/bin/debugserver
ssh root@{iOS IP}
chmod +x /usr/bin/debugserver
```
常看 库支持的架构 lipo -info {bin}

## 使用 debugserver

相关知识：
ssh 
scp
lipo
ldid

## reference
+ http://bbs.iosre.com/t/debugserver-lldb-gdb/65
+ http://www.cnblogs.com/ludashi/p/5730338.html
+ http://versprite.com/og/ios-reverse-engineering-part-one-configuring-lldb/


