---
layout: post
category: "iOS"
title: "iOS沙盒机制"
tags: [iOS]

---

本文主要介绍iOS沙盒机制已经沙盒的目录结构。

##沙盒机制
iOS应用程序都被独立于自己的空间，这个有点像进程的虚拟内存一样，应用程序之间不能互相访问，应用程序只能访问自己空间下的目录和文件，这个区域就叫做沙盒（sandbox）。   

综上所述，沙盒机制有以下特点：   

*   应用程序之间相互隔离
*   应用程序只能访问自己本地的内容，不能访问其他文件目录（越狱手机除外）
*   为应用程序构建了一个完整的运行空间
*   应用程序有自己的缓存和数据备份

不好的地方：
   
*   不能访问其他应用的文件(iOS8有所开放)

##沙盒目录结构：

###一个完整的应用程序的沙盒目录结构：   

*   Document    
	存放文稿以及其他文本数据，此目录可以与iTunes进行同步；
*   Libarary   
	存储程序的默认设置或其它状态信息；其中，Libaray目录下又有两个子目录Caches和Preference。
*   tmp   
	存放临时文件的位置，iPhone重启后，此目录文件将被自动移除；
*   xxx.app   
	bundle的路径，用来存放应用程序二进制文件，以及资源文件；

###获取目录：

Document:

	NSString *docPath = [NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) lastObject];

xxx.app:

	NSString* appPath = [[NSBundle mainBundle] BundlePath];

Libaray:

    NSString *libPath = [NSSearchPathForDirectoriesInDomains(NSLibraryDirectory, NSUserDomainMask, YES) firstObject]; 

tmp:

	NSString *tmpDir = NSTemporaryDirectory(); 


##iOS8的Extension
iOS8在苹果公司的努力下，稍微对沙盒机制做出了点让步，iOS8应用程序允许应用程序访问其他应用的数据，但仅仅包括：
Extension有多种类型，每一种类型都绑定到一个称为“扩展点（Extension point）”的系统区域：

*   “今日（Today，又称为Widget）”：可以快速获取更新或者在通知中心的今日视图中执行一项快速任务。
*   共享：发布到一个共享网站或者与其它应用程序共享内容。
*   动作：在另一个应用程序的上下文中操作或查看内容。
*   照片编辑（仅限于iOS）：在照片应用程序中编辑照片或视频。
*   查找器（仅限于iOS）：在查找器中直接显示文件同步的状态信息。
*   文档提供程序（仅限于iOS）：提供对文件库的访问和管理。
*   自定义键盘（仅限于iOS）：用自定义键盘替代iOS系统键盘，并用于所有的应用程序中。
