---
layout: post
title: '简单选择排序与堆排序——十大排序算法'
date: 2019-03-27
author: S-Lemon
tags: 算法
---

选择排序下的简单选择排序与堆排序的详细介绍



## 简单选择排序

> 选择排序的工作原理是每一次从待排序的数据元素中选出最小（或最大）的一个元素，存放在序列的起始位置，然后，再从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序序列的末尾。以此类推，直到全部待排序的数据元素排完。 选择排序是不稳定的排序方法。 

个人理解：最简单最常用也是最稳定的排序…………

![Selection Sort]({{ "/assets/img/SelectionSort.gif" | absolute_url }} "Selection Sort")

代码如下：

```java
@Test
    public void SelectionSort(){
        int minIndex = 0;
        for(int i = 0; i < array.length - 1; i++){
            minIndex = i;
            for(int j = i+1; j < array.length; j++){
                if(array[j] < array[minIndex]) minIndex = j;
            }
            if(minIndex != i){
                swap(minIndex, i);
            }
        }
        System.out.println("简单选择排序："+Arrays.toString(array));
    }
```

最佳情况：T(n) = O(n<sup>2</sup>)  最差情况：T(n) = O(n<sup>2</sup>)  平均情况：T(n) = O(n<sup>2</sup>) 

真稳定…………



## 堆排序

> **堆排序**（英语：Heapsort）是指利用堆这种数据结构所设计的一种排序算法。堆是一个近似完全二叉树的结构，并同时满足**堆积的性质**：即子结点的键值或索引总是小于（或者大于）它的父节点 。

个人理解：

​	大致思路说起来很简单，就是利用完全二叉树的性质，然后每次都将根节点与最后一个节点互换，这样最后一个节点就是最大的（按大顶堆来建树），然后除去最后一个节点，再继续建树，然后再换节点，直到只剩下两个节点为止。

​	因为之前没怎么接触过堆排序（但学过数据结构，对树还算比较熟悉），这个算法难点就在每次根节点与末节点互换后剩下的节点的构建成树的过程。

> - 将初始待排序关键字序列(R1,R2….Rn)构建成大顶堆，此堆为初始的无序区；
> - 将堆顶元素R[1]与最后一个元素R[n]交换，此时得到新的无序区(R1,R2,……Rn-1)和新的有序区(Rn),且满足R[1,2…n-1]<=R[n]；
> - 由于交换后新的堆顶R[1]可能违反堆的性质，因此需要对当前无序区(R1,R2,……Rn-1)调整为新堆，然后再次将R[1]与无序区最后一个元素交换，得到新的无序区(R1,R2….Rn-2)和新的有序区(Rn-1,Rn)。不断重复此过程直到有序区的元素个数为n-1，则整个排序过程完成。

![HeapSort]({{ "/assets/img/HeapSort1.gif" | absolute_url }})

代码如下：

```java
    @Test
    public void HeapSort(){
        length = array.length;
        buildHeap();
        while(length > 0){
            swap(0, length-1);
            length--;
            adjustHeap(0);
        }
        System.out.println("堆排序：" + Arrays.toString(array));
    }
    //构建大顶树
    public void buildHeap(){
        //利用for循环，从树的最后的非叶子节点开始[(length - 1)/2]，自底向上的调用adjustHeap()
        for(int i = (length - 1)/2; i >= 0; i--){
            adjustHeap(i);
        }
    }
    //传入leap，以leap为父节点比较子节点与其的大小，找出最大的那个并换到父节点位置
    //假如有swap操作，就需要递归重新adjustHeap()swap后的子树
    //(每层递归只比较一个节点与其至多的两个子节点)
    public void adjustHeap(int leap){
        int maxIndex = leap;
        //比较左子节点
        if(leap * 2 < length && array[leap*2] > array[maxIndex]){
            maxIndex = leap * 2;
        }
        //比较右子节点
        if(leap * 2 + 1 < length && array[leap*2+1] > array[maxIndex]){
            maxIndex = leap * 2 + 1;
        }
        //最大节点不是此节点，则与找到的最大值的子节点swap
        if(maxIndex != leap){
            swap(maxIndex, leap);
            adjustHeap(maxIndex);
        }
    }
```

此算法最关键的还是树的结构，然后利用大顶树的特性来选择出最大值并排序，相当于将简单交换排序的找到最小值过程换成找到构建大顶树。所以adjustHeap()函数才是关键。运用递归的思想，是很容易就能得到通过极限来求解的思路的！

最佳情况：T(n) = O(nlogn)  最差情况：T(n) = O(nlogn)  平均情况：T(n) = O(nlogn) 

## 参考文章

[https://blog.csdn.net/hellozhxy/article/details/79911867](https://blog.csdn.net/hellozhxy/article/details/79911867)



