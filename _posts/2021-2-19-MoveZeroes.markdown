---
layout: post
title:  "283. 移动零"
date:   2020-2-19 20:00:00
categories: LeetCode
---
题目描述

    给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。
    示例:
        输入: [0,1,0,3,12]
        输出: [1,3,12,0,0]
    说明:
        必须在原数组上操作，不能拷贝额外的数组。
        尽量减少操作次数。

#### 解题思路
从左往右遍历非零元素，记录非零元素的指针移动，最后补充非零元素指针与数组长度之间的零元素区域。
```java
public class MoveZeroes {

    public void moveZeroes(int[] nums) {
        int length = nums.length, index = 0;
        for (int i = 0; i < length; i++) {
            if (nums[i] != 0) {
                nums[index] = nums[i];
                index++;
            }
        }
        while (index < length) {
            nums[index] = 0;
            index++;
        }
    }

}
```

#### 官方解答
双指针
右指针遍历数组，左指针指向数组中第一个零元素的索引。每次右指针指向的非零元素时，与左指针指向的零元素交换位置。
时间复杂度：O(n)
空间复杂度：O(1)
```java
public void moveZeroes(int[] nums) {
    int n = nums.length, left = 0, right = 0;
    while (right < n) {
        if (nums[right] != 0) {
            swap(nums, left, right);
            left++;
        }
        right++;
    }
}

public void swap(int[] nums, int left, int right) {
    int temp = nums[left];
    nums[left] = nums[right];
    nums[right] = temp;
}
```

#### 小结
将数组改造为两部分，一部分为非零元素需要保证顺序，另一部分为零元素无顺序要求。这里提供两种解题思路：
    1. 把数组中的零元素剔除（压缩非零元素）最后再填充零元素。
    2. 遍历数组中的元素, 将排在零元素之后的非零元素与首位零元素交换位置。（官方解答更优，只需遍历一次数组）


leetcode原题链接：[283. 移动零](https://leetcode.com/problems/move-zeroes/)