---
layout: post
title:  "350. 两个数组的交集 II"
date:   2020-2-3 22:00:00
categories: LeetCode
---
题目描述

    给定两个数组，编写一个函数来计算它们的交集。

#### 解题思路
方法一：根据提示，先对两个数组进行了排序，然后定义两个个指针，分别用来遍历两个数组。另外再定义一个指针，用来填充结果数组。
```java
public class IntersectionOfTwoArraysII {

    public int[] intersect(int[] nums1, int[] nums2) {
        Arrays.sort(nums1);
        Arrays.sort(nums2);

        int length1 = nums1.length, length2 = nums2.length;
        int[] result = new int[Math.min(length1, length2)];
        int index = 0, index1 = 0, index2 = 0;
        while (index1 < length1 && index2 < length2) {
            int i1 = nums1[index1], i2 = nums2[index2];
            if (i1 == i2) {
                result[index] = i1;
                index++;
                index1++;
                index2++;
            } else if (i1 < i2) {
                index1++;
            } else {
                index2++;
            }
        }
        return Arrays.copyOfRange(result, 0, index);
    }

}
```
方法二：借助java的集合遍历，构造双重循环，在内层循环时将符合条件的元素移除。
```java
public int[] intersect1(int[] nums1, int[] nums2) {
    List<Integer> list1 = new ArrayList<>();
    for (int value : nums1) {
        list1.add(value);
    }

    List<Integer> list = new ArrayList<>();
    for (int i2 : nums2) {
        Iterator<Integer> it = list1.iterator();
        while (it.hasNext()) {
            if (it.next() == i2) {
                list.add(i2);
                it.remove();
                break;
            }
        }
    }
    return list.stream().mapToInt(i -> i).toArray();
}
```

#### 官方解答
方法一：哈希表
借助java的集合map，对其中一个较长的数组做元素计数，key为元素，value为元素出现的次数。遍历短数组时，将map集合中符合条件的元素的计数做修改。
时间复杂度：O(m+n)
空间复杂度：O(min(m,n))
```java
public int[] intersect(int[] nums1, int[] nums2) {
    if (nums1.length > nums2.length) {
        return intersect(nums2, nums1);
    }
    Map<Integer, Integer> map = new HashMap<Integer, Integer>();
    for (int num : nums1) {
        int count = map.getOrDefault(num, 0) + 1;
        map.put(num, count);
    }
    int[] intersection = new int[nums1.length];
    int index = 0;
    for (int num : nums2) {
        int count = map.getOrDefault(num, 0);
        if (count > 0) {
            intersection[index++] = num;
            count--;
            if (count > 0) {
                map.put(num, count);
            } else {
                map.remove(num);
            }
        }
    }
    return Arrays.copyOfRange(intersection, 0, index);
}
```

方法二：排序+双指针
跟我的解题思路【方法一】相同
时间复杂度：O(mlogm+nlogn)
空间复杂度：O(min(m,n))

#### 小结
当nums2的元素存储在磁盘上，且磁盘内存有限无法一次性加载元素到内存中时，无法高效地对nums2进行排序，因此推荐hash表的方式
——参考自官方解答


leetcode原题链接：[350. 两个数组的交集 II](https://leetcode.com/problems/intersection-of-two-arrays-ii/)