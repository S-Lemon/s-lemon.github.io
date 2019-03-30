---
layout: post
title: '冒泡排序与快速排序——十大排序算法'
date: 2019-03-26
author: S-Lemon
tags: 算法
---

交换排序下的冒泡排序与快速排序的详细介绍



## 前言

> **若存在常量k和n0,使算法A在解决规模n>=n0的问题时，需要的问题单元不大于k\*f(n),则算法A为f(n)阶，表示为O(f(n))** 



## 冒泡排序

> 冒泡排序就是重复地走访过要排序的元素列，依次比较两个相邻的元素，如果他们的顺序（如从大到小、首字母从A到Z）错误就把他们交换过来。走访元素的工作是重复地进行直到没有相邻元素需要交换，也就是说该元素已经排序完成。 

个人理解：冒泡排序就是跟泡泡冒出来一样，每次遍历数组时，将大的数不断的往后面推，最终实现从小到大的排序，因此需要两层循环，外层循环代表一共要循环遍历数组多少次，内层循环是在每次遍历列表时，需要在剩下的没排序的数中，遍历比较相邻数的大小并交换排序。

![冒泡排序]({{ "/assets/img/Bubblesort.gif" | absolute_url }} "动态图")

代码如下：

```java
int[] array = {3, 44, 38, 5, 47, 15, 36, 26, 27, 2, 46, 4, 19, 50, 48};
@Test
public void TestBubbleSort(){
    for(int i = 0; i < array.length; i++){               //外层循环（即总的需要遍历多少次数组）
        for(int j = 0; j < array.length - 1 - i; j++ ){  //内层循环（array.length-1-i每次遍历
													//         数组时让排好的不用再排）
            if(array[j] > array[j+1]){                   //内层循环中对相邻的两数比较换位
                int temp = array[j];
                array[j] = array[j+1];
                array[j+1] = temp;
            }
        }
    }
    System.out.print("冒泡排序：");
    for(int i = 0; i < array.length; i++){
        System.out.print(array[i] + "  ");
    }
}
```

最佳情况：T(n) = O(n)   最差情况：T(n) = O(n<sup>2</sup> )   平均情况：T(n) = O(n<sup>2</sup>) 



## 快速排序

> 通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。 

个人理解：快速排序跟冒泡排序都是同属于交换排序，只是思路不太一样。快速排序突出的是一个递归思想，将数组分区（按基准数进行比较，大的为一区，小的为一区），按递归思想来，当分区分到极限时，就是有序的两个数，至此，整个数组也会变得有序。

![QuickSort]({{ "/assets/img/Quicksort.gif" | absolute_url }} "QuickSort")

代码如下：

```java

@Test
	//测试函数
    public void TestQuickSort(){
        System.out.print("快速排序：");
        QuickSort(0, array.length-1);		//调用快速排序函数
        for(int i = 0; i < array.length; i++){
            System.out.print(array[i] + "  ");
        }
    }
    public void QuickSort(int start, int end){
        if(start >= end){return;}            //递归出口
        int low, high, pivot;
        low = start;
        high = end;
        pivot = array[start];               //基准数，一般为分区的第一个数，也可用 
        								 //array[(int)Math.random()*(end-start+1)]
        while(low < high){				   //以基准数为准，分成大小两区
            while(low < high && array[high] >= pivot)high--;	//从右往左找到小于基准数的数
            while(low < high && array[low] <= pivot)low++;		//从左往右找到大于基准数的数
            if(low < high){
                swap(low, high);							  //交换两数
            }
        }
        swap(start, low);				  //将基准数复位,执行后基准数下标为low（注）
        QuickSort(start, low-1);		   //递归调用，小区（start~low-1）重新调用快速排序
        QuickSort(low+1, end);			   //大区(low+1~end)重新调用快速排序
    }
	
	//两数交换函数
    public void swap(int i, int j){
        int temp;
        temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }
```

注：为什么要将array[start]跟array[low]调换呢？为什么不是low +/- 1? 首先，前面用的是先从右往左找high，所以当while里high跟low碰头时，一定是先high碰到low，而low不会动的情况，所以此时的array[low]一定比pivot小，就要互换。

最佳情况：T(n) = O(nlogn)   最差情况：T(n) = O(n2)   平均情况：T(n) = O(nlogn) 



##参考文章

[https://blog.csdn.net/hellozhxy/article/details/79911867](https://blog.csdn.net/hellozhxy/article/details/79911867)

[快速排序（过程图解）](https://blog.csdn.net/adusts/article/details/80882649)

