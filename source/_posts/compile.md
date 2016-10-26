---
title: The Compiler is Mine Friend
date: 2016-04-11 16:48:22
categories: Tool
tags: 
- GCC 
- Objective
- Xcode
keywords: Xcode, complier
description: 充分利用编译为我们提供的便利，可以极大的改善我们的工作效率。我喜欢和大家交朋友，我相信朋友会在关键时候给我提示的。
---

## Apple LLVM compiler 

### Warning Flag 语法
+ -Wfoo 开启 foo，foo表示一类或者一组警告
+ -Wno-foo 关闭 foo 警告
+ -w 关闭所有的警告

### 设置 Warning = Errors
//.xccongig 
GCC_TREAT_WARNINGS_AS_ERRORS = YES
// cms-ling 
-Werror

### 编译器给出的几类警告：
+ A valid issue => Fix the issue
+ 你不关心的，或者无意义的警告 => 关闭 局部或者全局 警告
+ 你不理解的警告 => 弄明白，否者你永远不明白

### 常见的警告组合
-Wall
-Wextra
-Wpedantic
-Weverything
-Wshadow 
``` C++
    int main(int argc, char *argv[]) {
        if ( 1 == 1 ) {
            int argc = 9;
            printf("integere is %d", argc);
        }
    }
```
-Wfloat-equal 浮点数相等比较
``` c++
float a = 2.0
flaot b = 3.1
if (a == b) {
    // TODO
}
```
-Wundef #if 中使用了未定义的符号
``` C
#if THIS_HAS_NOT_BEEN_DEFINED
```

-Wempty-body if else do while 不会执行的代码段
``` C++
if (1 == 2) {
    // TODO
} else {
    // When invoke?
}
```

-Wnewline-eof 文件的结尾符不是空行

Clang 中新的 警告 类型
-Wobjc-literal-compare
-Warc-repeated-use-of-weak

### 关闭 警告

``` Objective-C
#pragma clang diagnostic push
#pragma clang diagnostic ignore "-Wstupid-method-name"

- (BOOL)doTheThingWithTheOtherThing {
    // TODO
}

#pragma clang diagnostic pop

- (void)doThingWithObject(NSObject * __attribute__((unused)))thingie {
    // TODO
}

- (void)doThingWithObject(NSObject * __unused)thingie {
    // TODO
}

- (void)doThingWithObject(NSObject *)thingie {
    #pragma unused(thingie)
    // TODO
}
```

add Complier Flags -W

## Function Attribute __attribute__ ((attribute-list))

## reference
+ https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html
+ https://gcc.gnu.org/onlinedocs/gcc/Diagnostic-Pragmas.html
+ http://clang.llvm.org/docs/UsersManual.html#options-to-control-error-and-warning-messages



