---
layout: post
category: "iOS"
title:  "仿QQ好友列表折叠效果"
tags: [iOS]

---

本文主要介绍QQ好友列表折叠效果的实现过程。

###原理

类似于QQ列表折叠效果做法其实很简单，其核心思想就是利用tableView的section header作为一级菜单，section内部的数据作为二级菜单展示，当展开section时，调用[tableView reload]重新刷新tableView，而在   
	
	- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section 
			
协议中，判断当前节点是否被展开，如果是，返回section个数，否则返回0，这样，很巧妙的的利用了tableView的特性来完成了折叠效果，很神奇。

###具体步骤

1. 设置header view

很简单
，利用协议   
	
	-(UIView *)tableView:(UITableView *)tableView viewForHeaderInSection:(NSInteger)section

来给tableView设置header，这些就是header：

![tableView headerView](../resources/IMG_0983.jpg)   

2. 保存某个section的展开状态
3. 利用协议设置每个section的row，关键点：被折叠的返回0，否则返回正常个数，如：

		- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {

    		NSString *indexStr = [NSString stringWithFormat:@"%ld", section];
    
    		BOOL isFolder = [selectedArr containsObject:indexStr];
   		 	NSInteger number = 0;
    		if (!isFolder) {
        		return 0;
    		}else{
        		GroupDataModel * array = [_arrayData objectAtIndex:section];
        		return array.groupData.count;
    		}
    
    		return number;
		}


###代码实现

见github地址：<https://github.com/anlong2008/ExpandTableView>


