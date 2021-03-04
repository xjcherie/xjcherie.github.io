---
layout: post
title:  "122. 买卖股票的最佳时机 II"
date:   2020-1-20 21:00:00
categories: LeetCode
---
题目描述

    给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。
    设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。
    注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

#### 解题思路
在给定的数组中，找到每一个有差值的区间，且左边界要小于右边界。
```java
public class BestTimeToBuyAndSellStockII {

    public int maxProfit(int[] prices) {
        int profit = 0;
        int leftIndex, rightIndex, index = 0;
        int length = prices.length;

        while (index < length) {
            leftIndex = index;
            while (index < length && prices[leftIndex] >= prices[index]) {
                leftIndex = index;
                index++;
            }
            rightIndex = leftIndex;
            while (index < length && prices[rightIndex] <= prices[index]) {
                rightIndex = index;
                index++;
            }
            if (leftIndex == rightIndex) {
                index++;
            }

            profit += Math.max(0, prices[rightIndex] - prices[leftIndex]);
        }
        return profit;
    }

    @Test
    public void test() {
        assertThat(maxProfit(new int[]{7, 1, 5, 3, 6, 4}), equalTo(7));
        assertThat(maxProfit(new int[]{1, 2, 3, 4, 5}), equalTo(4));
        assertThat(maxProfit(new int[]{7, 6, 4, 3, 1}), equalTo(0));
        assertThat(maxProfit(new int[]{6, 1, 3, 2, 4, 7}), equalTo(7));
    }

}
```

#### 官方解答
方法一：动态规划


方法二：贪心
如果股票当天没变动，那么做T是没用的，也就是买卖不影响收益。

#### 小结


leetcode原题链接：[122. 买卖股票的最佳时机 II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii)