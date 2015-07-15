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
  NSObject提供了诸如performSelector***的方法来创建子线程。     `   

    其中，最重要的是performSelectorInBackground:withObject:这个方法，他用法类似NSThread的detachNewThreadSelector:toTarget:withObject:，方法原型：      
    `- (void)performSelectorInBackground:(SEL)aSelector withObject:(id)arg NS_AVAILABLE(10_5, 2_0);`

    如：   
    `[self performSelectorInBackground:@selector(threadPro:) withObject:nil];`   
  NSObject起线程最大的优点是不用新创建任何对象就可以起一个工作线程。
    
### POSIX Thread   

    Mac OS 10.4和iOS2.0引入了POSIX库，这样就让创建线程变的更加灵活了，你既可以用Cocoa Api也可以用POSIX API。
    创建线程API：  
      `int pthread_create(pthread_t * __restrict, const pthread_attr_t * __restrict, void *(*)(void *), void * __restrict);`   
    具体使用方法参考POSIX API吧

### NSOperation 和 NSOperationQueue
### GCD


## 线程池的概念
