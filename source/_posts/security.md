title: Security
date: 2015-11-07 18:53:13
categories: Dictionary
tags:
- Security
description: 利益，好奇都是对安全造成威胁的原因，本文对于原因不感兴趣，主要是介绍目前计算机科学中运用的信息安全技术。由于本人的知识有限，涉及不深，故在此抛砖引玉。
keywords: secturity,encrypt,authorization
------
<!--more-->
---------
## 专有名词
+ 信息（information, message）：定义很多，建议查看维基百科，简单理解为信息是某个主体关注的东西。
+ 安全（security ）:
+ centification authorization authentification audit 
encrypt decrypt abstract
cryptogram

## 安全技术

加密<=>解密
摘要算法 MD5 SHA
对称加密解密算法
DES
非对称加密解密算法
RSA
常用安全策略
常用安全协议
TSL SSL
数据结构
x.509 v3
安全组织结构
PKI
安全软件
openSSL

## 代码签名
codesign
secutity
openssl
uzip
md5 / sha

### 查看可以使用的签名证书
```
    security find-identity -v -p codesiging
```
### 查看mobilprovision 
security cms -D -i embedded.mobileprovision
