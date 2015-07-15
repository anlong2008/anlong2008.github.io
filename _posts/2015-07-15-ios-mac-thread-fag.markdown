---
layout: post
category: "iOS"
title:  "iOS/Mac OS X系统下的并发"
tags: [iOS]
---

## 为什么需要线程
## iOS/Mac OS下创建线程的方法

1. NSThread  
NSThread提供了两种方法创建线程：  
*   调用NSThread的start消息，如；  
`NSThread *thread = [[NSThread alloc] initWithTarget:self selector:@selector(threadPro:) object:nil];`  
`[thread start];`  
*   直接用NSThread类方法 + (void)detachNewThreadSelector:(SEL)selector toTarget:(id)target withObject:(id)argument; 创建并启动线程，如；  
`[NSThread detachNewThreadSelector:@selector(threadPro:) toTarget:self withObject:nil];`
2. NSObject
3. POSIX Thread
4. NSOperation 和 NSOperationQueue
5. GCD


## 线程池的概念
