---
layout: post
title:  "217. 存在重复元素（easy，可忽略）"
date:   2020-2-2 21:00:00
categories: 算法
---
题目描述

    给定一个整数数组，判断是否存在重复元素。
    如果存在一值在数组中出现至少两次，函数返回 true 。如果数组中每个元素都不相同，则返回 false 。

#### 解题思路
将数组放在set中，只要数量不一样就说明存在元素重复
```java
public class ContainsDuplicate {

    public boolean containsDuplicate(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for (int num : nums) {
            set.add(num);
        }
        return nums.length != set.size();
    }

}
```

#### 官方解答
方法一：排序
分两步，先做排序，后比较相邻元素是否相同。
时间复杂度：O(N\log N)
空间复杂度：O(logN)
```java
public boolean containsDuplicate(int[] nums) {
    Arrays.sort(nums);
    int n = nums.length;
    for (int i = 0; i < n - 1; i++) {
        if (nums[i] == nums[i + 1]) {
            return true;
        }
    }
    return false;
}
```

方法二：哈希表
跟我的解题思路相同，只是在给哈希表添加元素的时候，就先做了判断
时间复杂度：O(N)
空间复杂度：O(N)
```java
public boolean containsDuplicate(int[] nums) {
    Set<Integer> set = new HashSet<Integer>();
    for (int x : nums) {
        if (!set.add(x)) {
            return true;
        }
    }
    return false;
}
```

#### 小结
刚开始做，以为会有比较巧妙的解题思路，想了五分钟没想出来，就用最省事的方式先做了。结果官方也没给比较新颖的思路。。。


leetcode原题链接：[217. 存在重复元素](https://leetcode.com/problems/contains-duplicate/)