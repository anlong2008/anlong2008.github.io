---
layout: post
category: "算法"
title: "归并排序"
tags: [算法]

---		
		
本文主要记录归并排序的算法原理已经代码实现

###算法原理

适用场景：两个或者多个有序表，要和成一张有序表。
算法核心思想：
从第0位开始，分别取出两张表中还没有排过序的最小的数字比较，比较后，将结果中最小的放入另外一张有序表中，依次类推，直到有一张表中没有数据了，将另外一张表剩余未排序的数据复制到第三张表中，至此，算法结束。
  
					
	void MegerSort(int a[], unsigned int aCount, int b[], unsigned int bCount, int result[], int& resultCount)
	{
    	// pa pb 分别指向a b初始位置
    	int *pa = a;
    	int *pb = b;
    	int *pResult = result;
    	int resultCount = aCount + bCount;
    	int sumCount = resultCount;
    	while (sumCount--) {
        if (*pa < *pb) {
            *pResult = *pa;
            pa ++;
            
        }else{
            *pResult = *pb;
            pb ++;
        }
        pResult ++;
        // 检查其中一个是否已经检查完毕
        if ((pa - a) > aCount) {
            while ((pb - b) < bCount) {
                *pResult = *pb;
                pb ++;
            }
            break;
        }
        
        if ((pb - b) > bCount) {
            while ((pa - a) < aCount) {
                *pResult = *pa;
                pa ++;
            }
            break;
        }
    }


测试代码：

	int main(int argc, const char * argv[]) {
    
    	int a[] = { 1, 3, 5, 7, 9 };
    	int b[] = {2, 4, 6, 8, 10 };
   	 	int c[10];
    	int cCount;
    
    	MegerSort(a, 5, b, 5, c, cCount);
    	return 0;
	}