---
layout: post
title:  "26. 删除排序数组中的重复项"
date:   2020-1-21 20:37:09
categories: LeetCode
---
题目描述

    给定一个排序数组，你需要在 原地 删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。
    不要使用额外的数组空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。

#### 解题思路
相同的元素都相邻，用一个指针单独记录不同元素的索引，然后让数组的元素相互比较是否处于同一类元素区域中。
每次for循环都是一个新的元素，while过滤相同元素。
    
```java
public class RemoveDuplicatesFromSortedArray {

    public int removeDuplicates(int[] nums) {
        int index = 0;
        for (int i = 0; i < nums.length; i++) {
            while (i + 1 < nums.length && nums[i] == nums[i + 1]) {
                i++;
            }
            nums[index] = nums[i];
            index++;
        }
        return index;
    }

    @Test
    public void test() {
        assertThat(removeDuplicates(new int[]{1, 1, 2}), equalTo(2));
        assertThat(removeDuplicates(new int[]{0, 0, 1, 1, 1, 2, 2, 3, 3, 4}), equalTo(5));
    }

}
```

#### 官方解答
每次循环，只要比较指针与循环的具体值是否相同，便可确定是否需要替换。
```java
public int removeDuplicates(int[] nums) {
    if (nums.length == 0) return 0;
    int i = 0;
    for (int j = 1; j < nums.length; j++) {
        if (nums[j] != nums[i]) {
            i++;
            nums[i] = nums[j];
        }
    }
    return i + 1;
}
```

#### 小结
我与官方解题思路的不同之处在于，官方利用到了指针元素，让其与具体循环的元素值做了比较。

leetcode原题链接：[26. 删除排序数组中的重复项](https://leetcode.com/problems/remove-duplicates-from-sorted-array)