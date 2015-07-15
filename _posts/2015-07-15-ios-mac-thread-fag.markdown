---
layout: post
category: "iOS"
title:  "iOS/Mac OS X系统下的并发"
tags: [iOS]
---

## iOS/Mac OS下创建线程的方法

### NSThread  
  NSThread提供了两种方法创建线程：  
    1.   调用NSThread的start消息，如；  
`NSThread *thread = [[NSThread alloc] initWithTarget:self selector:@selector(threadPro:) object:nil];`  
`[thread start];`  
    2.   直接用NSThread类方法 + (void)detachNewThreadSelector:(SEL)selector toTarget:(id)target withObject:(id)argument; 创建并启动线程，如；  
`[NSThread detachNewThreadSelector:@selector(threadPro:) toTarget:self withObject:nil];`   

### NSObject
  NSObject提供了诸如performSelector***的方法来创建子线程。   
    `- (void)performSelectorOnMainThread:(SEL)aSelector withObject:(id)arg waitUntilDone:(BOOL)wait modes:(NSArray *)array;`   
  `- (void)performSelectorOnMainThread:(SEL)aSelector withObject:(id)arg waitUntilDone:(BOOL)wait;`   
  `- (void)performSelector:(SEL)aSelector onThread:(NSThread *)thr withObject:(id)arg waitUntilDone:(BOOL)wait modes:(NSArray *)array NS_AVAILABLE(10_5, 2_0);`   
  `- (void)performSelector:(SEL)aSelector onThread:(NSThread *)thr withObject:(id)arg waitUntilDone:(BOOL)wait NS_AVAILABLE(10_5, 2_0);`   
  `- (void)performSelectorInBackground:(SEL)aSelector withObject:(id)arg NS_AVAILABLE(10_5, 2_0);`   

其中，最重要的是performSelectorInBackground:withObject:这个方法，他用法类似NSThread的detachNewThreadSelector:toTarget:withObject:，如：   
    `[self performSelectorInBackground:@selector(threadPro:) withObject:nil];`
### POSIX Thread
### NSOperation 和 NSOperationQueue
### GCD


## 线程池的概念
