---
layout: post
category: "iOS"
title:  "iOS/Mac OS X系统下的并发"
tags: [iOS]
---

本文旨在总结iOS应用层创建线程的方法。

### NSThread  
  NSThread提供了两种方法创建线程：  
  1. 调用NSThread的start消息，如；  
  
        NSThread *thread = [[NSThread alloc] initWithTarget:self selector:@selector(threadPro:) object:nil];     
        [thread start];  

  2. 直接用NSThread类方法 + (void)detachNewThreadSelector:(SEL)selector toTarget:(id)target withObject:(id)argument; 创建并启动线程，如；
  
        [NSThread detachNewThreadSelector:@selector(threadPro:) toTarget:self withObject:nil];    

### NSObject   
  NSObject提供了诸如performSelector***的方法来创建子线程。     `   

  其中，最重要的是performSelectorInBackground:withObject:这个方法，他用法类似NSThread的detachNewThreadSelector:toTarget:withObject:，方法原型：

        -(void)performSelectorInBackground:(SEL)aSelector withObject:(id)arg NS_AVAILABLE(10_5, 2_0);

  如：   
        
        [self performSelectorInBackground:@selector(threadPro:) withObject:nil];   
  
  NSObject起线程最大的优点是不用新创建任何对象就可以起一个工作线程。
    
### POSIX Thread   

  Mac OS 10.4和iOS2.0引入了POSIX库，这样就让创建线程变的更加灵活了，你既可以用Cocoa Api也可以用POSIX API。
  创建线程API：  
  
        int pthread_create(pthread_t * __restrict, const pthread_attr_t * __restrict, void *(*)(void *), void * __restrict);   
        
  具体使用方法参考POSIX API吧

### NSOperation 和 NSOperationQueue  
  
  一般情况下，线程能够帮我们处理一些比较耗时的工作，但线程并不是越多越好，很多时候，我们需要手动去控制线程的并发量，这时候，NSOperationQueue登场了。
  OperationQueue的并发度是可以通过如下方式进行设置:   
  
        -(void)setMaConcurrentOperationCount:(NSInteger)count  
        
  NSOperation 和 NSOperationQueue创建线程的方法：
  NSOperation（继承NSOperation去扩展我们的操作）可以封装我们的操作，然后将创建好的NSOperation对象放到NSOperationQueue中，OperationQueue便开始启动新的线程去执行队列中的操作。   
  
### GCD

  GCD(Grand Central Dispatch)是libdispatch这个开源项目，此方法创建线程最大的优势是可以将我们的操作在线程中有序执行，并且切换线程很方便。   
  如：我们在工作线程中从网络下载一个图片资源，下载完成后，需要在主线程去更新UI。    
  
        dispatch_queue_t imageDownloadQueue = dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0);     
          dispatch_async(imageDownloadQueue, ^{   
                NSURL *imageURL = [NSURL URLWithString:@"http://test.com/test.png"];   
               NSData *imageData = [NSData dataWithContentsOfURL:imageURL];  
                UIImage *image = [UIImage imageWithData:imageData];   
               dispatch_async(dispatch_get_main_queue(), ^{   
                    [imageView setImage:image];//UIKit必须在主线程执行    
                });  
            });   
