---
layout: post
title: '归并排序——十大排序算法'
date: 2019-03-30
author: S-Lemon
tags: 算法
---

今日来介绍归并排序，归并排序还算是属于比较排序的一种，具体的有二路排序跟多路排序

## 归并排序

> 归并排序（MERGE-SORT）是建立在归并操作上的一种有效的排序算法,该算法是采用分治法（Divide and Conquer）的一个非常典型的应用。将已有序的子序列合并，得到完全有序的序列；即先使每个子序列有序，再使子序列段间有序。若将两个有序表合并成一个有序表，称为二路归并。 

个人理解：

​	复习完整个比较排序了，泪目…… 好啦，先说说归并排序，首先就是要对递归熟悉，这样看这个就很简单了，我看了下面的动态图一个过程，然后跟算法思想就差不多了解这个算法是怎么跑的了。

​	首先就是分治法，感觉其他排序也有这个一部分的思想，只是后期组装起来不一样而已。分治法核心就是“分”、“治”、“合”。“分就是将一个大问题分成一个个小问题”，“治”就是将各个小问题逐个攻破，“合”就是将各个被解决的小问题合并起来，并解决一开始的母问题。

​	所以一开始就调用MergeSort将一个大的问题不断递归分解成小问题，那如何解决跟合并呢，也就是说MergeSort是最顶层，然后递归细化问题，细化到最后，问题已经无法再被细化了，那么就要解决了，这时就要对问题进行解决了，这个解决方案还要兼顾一个，合并过程中的问题的解决，所以这时从动态图可以很清楚的得知，我们一开始是对各个小数组有过排序的，那么数组顶端的一定是最小的，每次比较顶端就行了。

![MergeSort]({{ "/assets/img/MergeSort.gif" | absolute_url }})



代码如下：

```java
    @Test
    public void MergeSortTest(){
        int[] result = MergeSort(array);
        System.out.println("归并排序：" + Arrays.toString(result));

    }

    public int[] MergeSort(int[] arr){
        if(arr.length < 2) return arr;
        int mid = arr.length/2;
        int[] left = Arrays.copyOfRange(arr, 0, mid);
        int[] right = Arrays.copyOfRange(arr, mid, arr.length);
        return merge(MergeSort(left), MergeSort(right));
    }

    public int[] merge(int[]left, int[]right){
        int[] result = new int[left.length+right.length];
        for(int index = 0, i =0, j = 0; index < result.length; index++){
            //left跑完
            if(i >= left.length){
                result[index] = right[j++];
            }
            //right跑完
            else if(j >= right.length){
                result[index] = left[i++];
            }
            //对数组顶端比较
            else if(left[i] > right[j]){
                result[index] = right[j++];
            }
            else result[index] = left[i++];
        }
        return result;
    }
```

最佳情况：T(n) = O(n)  最差情况：T(n) = O(nlogn)  平均情况：T(n) = O(nlogn) 



## 参考文章

[https://blog.csdn.net/hellozhxy/article/details/79911867](https://blog.csdn.net/hellozhxy/article/details/79911867)







