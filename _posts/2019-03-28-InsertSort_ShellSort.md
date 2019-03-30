---
layout: post
title: '插入排序与希尔排序——十大排序算法'
date: 2019-03-28
author: S-Lemon
tags: 算法
---

今日记的是——插入排序与希尔排序（又是排序的一天……）

## 插入排序

> 插入排序的基本思想是：每步将一个待排序的记录，按其关键码值的大小插入前面已经排序的文件中适当位置上，直到全部插入完为止。 

个人理解：感觉这个算法拿来用在一个有序的数组中插入一个数值，使新数组有序这种情况比较正常吧。算法内容的话没什么特别需要注意的，就是不断的将数组分成两部分（第一部分有序，第二部分无序），不断从第二部分抽出一个插到第一部分合适的位置中。上图感觉比较好理解吧……

![InsertSort]({{ "/assets/img/InsertSort.gif" | absolute_url }})

代码如下：

```java
	@Test
    public void InsertSort(){
        int cur;
        for(int i = 1; i < array.length; i++){
            cur = array[i];
            int pre = i - 1;
            while (pre >= 0 && array[pre] > cur ){
                array[pre+1] = array[pre];
                pre--;
            }
            array[pre+1] = cur;
        }
        System.out.println("插入排序："+Arrays.toString(array));
    }
```

最佳情况：T(n) = O(n)   最坏情况：T(n) = O(n<sup>2</sup>)   平均情况：T(n) = O(n<sup>2</sup>) 



## 希尔排序

> **希尔排序**(Shell's Sort)是插入排序的一种又称“缩小增量排序”（Diminishing Increment Sort），是直接插入排序算法的一种更高效的改进版本。希尔排序是非稳定排序算法。
>
> 希尔排序是把记录按下标的一定增量分组，对每组使用直接插入排序算法排序；随着增量逐渐减少，每组包含的关键词越来越多，当增量减至1时，整个文件恰被分成一组，算法便终止。 

个人理解：直接点的说，就是将一个数组按一定的增量(group)分成几(length/group)组，然后对组内进行插入排序，然后将增量逐渐减少(一般都是对半减少)，直到增量变为1时，整个数组分为一组，再插入排序，算法over。

 ![ShellSort]({{ "/assets/img/ShellSort.jpg" | absolute_url }})



代码如下：

```java
@Test
    public void ShellSort(){
        int cur;
        int group = array.length / 2;		//group为增量
        while(group > 0){
            //for循环内，就是不断对每个组的组内数组进行插入排序，每次循环只处理一组内的一次插入
            for(int i = group; i < array.length; i++){
                cur = array[i];
                int pre = i - group;
                //while循环是对组内数据的对比与后移（原理跟上面的插入排序一模一样）
                while(pre >= 0 && array[pre] > cur){
                    array[pre+group] = array[pre];
                    pre -= group;
                }
                array[pre+group] = cur;
            }
            group = group/2;
        }
        System.out.println("希尔排序："+Arrays.toString(array));
    }
```

最佳情况：T(n) = O(nlog<sub>2</sub> n)  最坏情况：T(n) = O(nlog<sub>2</sub> n)  平均情况：T(n) =O(nlog2n) 



## 参考文章

[https://blog.csdn.net/hellozhxy/article/details/79911867](https://blog.csdn.net/hellozhxy/article/details/79911867)

