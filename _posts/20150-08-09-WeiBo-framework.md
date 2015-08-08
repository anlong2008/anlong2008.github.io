---
layout: post
category: "iOS"
title:  "微博社交类项目中可以用的第三方库"
tags: [iOS]

---

本文主要介绍我在微博社交类项目中用到的第三方库，仅供参考
不分先后顺序   

| framework        | 简介           |
| ------------- |-------------	 |
| [MBProgressHUD](https://github.com/jdg/MBProgressHUD)  |  用于替代系统指示器的控件，俗称loading页面，可以提供丰富的显示效果，如带文本、带进度、浮层提示等 | 
| [SDWebImage](https://github.com/rs/SDWebImage)      | 用于对从 Web 端接受到的图片进行缓存, 是 UIImageView 的扩展, 应用起来比较简单      |    
| [AFNetworking](https://github.com/AFNetworking/AFNetworking) | 非常好用的http请求库，提供了多种api，总有一款适合你      |     
| [oAuthComsumer](https://github.com/jdg/oauthconsumer) | oAuth或者xAuth认证的时候可以计算签名值 |
| [ShareSDK](http://mob.com/Download/detail?type=1&plat=2) | 一键分享,支持分享文字、图片、图文、音乐、视频、链接，可一键分享至微信、微博、Facebook、Twitter等多个平台；支持@好友和话题功能。轻松实现你分享出去的链接中，仅让用户看到您的官网地址，而并非ShareSDK。|
| [AutoHyperlinks](https://github.com/ByteProject/AutoHyperlinks.framework) | 用于微博正文检测超链接的库，如检测@，##，都非常有用 |
| [NJKWebViewProgress](https://github.com/ninjinkun/NJKWebViewProgress)| 打开超链接时可以出现进度条效果，进度是假的，因为设计到真实进度需要用到private api, 看到主页介绍说facebook、雅虎都用它|
| [SDRefreshView ](https://github.com/gsdios/SDRefreshView)| 用于tableView下拉刷新的控件，也很好用 |
| LGtitleBarView| 仿网易新闻二级菜单做的左右切换的效果 |


由于本人在在开发过程中，所以会持续更新。