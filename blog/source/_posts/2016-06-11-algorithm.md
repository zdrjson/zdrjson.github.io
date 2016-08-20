---
layout: post
title: "Algorithm"
date: 2016-06-11 16:32:19 +0800
comments: true
categories: 
---


#二分查找
```
//二分查找又称折半查找，优点是比较次数少，查找速度快，平均性能好；其缺点是要求待查表为有序表，且插
入删除困难。因此，折半查找方法适用于不经常变动而查找频繁的有序列表。
//递归方法
int binarySearch1(int a[], int low, int high, int findNum) {
    int mid = (low + high) / 2;
    if (low > high) {
        return -1;
    }
    else{
        if (a[mid] > findNum) {
            return binarySearch1(a,low,mid - 1,findNum);
        } else if (a[mid] < findNum){
            return binarySearch1(a,mid +1, high, findNum);
        } else {
            return mid;
        }
    }
}
//非递归方法
int binarySearch2(int a[], int low, int high, int findNum) {
    while (low <= high) {
        int mid = (low + high) / 2; //此处一定要放在while里面
        if (a[mid] < findNum) {
            low = mid + 1;
        } else if (a[mid] > findNum){
            high = mid - 1;
        } else {
            return mid;
        }
    }
    return -1;
}
```

